<template>
<!--  3D Globe Map -->
  <div id="globeViz"></div>
</template>

<script>
import * as d3 from "d3";
import Globe from "globe.gl";

export default {
  name: "SSAViewer",
  components: {},
  props: ["width","height"],
  data: function() {
    return{
      world: null,
      mapcenter: { ssa: {lat: -5, lng: 15, altitude: 1.5},
                  ch: {lat:47, lng:15, altitude:0.8}},
      rotationSpeed: 0.85,
      deathRateColorScale: d3.scaleSequentialSqrt(d3.interpolateRgbBasis( ["#03dafd","#fff","#ffe600"])),
      deathRateColumn: '2017_death_rate',
      deathRateFilePath: 'data/hiv-death-rates.geojson',
      infectionColumn:'2017-_hiv_share',
      infectionFilePath:'data/hiv_infection_rate.geojson',
      infectionColorScale: d3.scaleSequentialSqrt(d3.interpolateRgbBasis(["#ffffff","#e00101","#780000"])),
      flagEndpoint:'https://corona.lmao.ninja/assets/img/flags', //url to get country flags
    }
  },
  methods: {
    initMap(){
      // Initialize the globe
      this.world = Globe()(document.getElementById('globeViz'))
        .showGlobe(false)
        .showAtmosphere(false)
        .backgroundColor('#FFFFFF')
        .lineHoverPrecision(0)
        .width(this.width)
        .height(this.height)
        .pointOfView({lat:0,lng:0, altitude:1.75}, 4000);
      this.showInfectionRate();
      this.autoRotate(true);
    },

    getToolTip(d, colName, title){
      // Show the tooltip when mouse hovering on polygons
      let flagName = d.ISO_A2.toLowerCase();
      if (d.ADMIN === 'France') {
        flagName = 'fr';
      } else if (d.ADMIN === 'Norway') {
        flagName = 'no';
      } else if (d.ADMIN === 'Taiwan,China') {
        flagName = 'cn'
      }
      let div_html = `<div class="globe-viewer-tooltip-container">
                        <img class="flag-img" src="${this.flagEndpoint}/${flagName}.png"/>
                        <div class="country-title">${d.ADMIN}</div>
                        <div class="description">
                            GDP: $<i>${this.numberWithCommas(d.GDP_MD_EST)}</i> Million<br/>
                            Population: <i>${this.numberWithCommas(d.POP_EST)}</i><br/>
                            ${title} 2017: <i>${d[colName].toFixed(2)}</i><br/>
                        </div>
                      </div>`

      return div_html;
    },
    numberWithCommas(x) {
      // Format numbers: 1,000,000,000
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },

    resizeMap(height, width){
      // Resize the globe
      this.world.width([width]);
      this.world.height([height]);
    },
    zoomToRegion(regionName){
      // Zoom to a region
      this.setPointOfView(this.mapcenter[regionName]);
      this.autoRotate(false);
    },
    setPointOfView(mapCenterPoint){
      // set the center point of map
      this.world.pointOfView(mapCenterPoint, 4000);
    },

    showDeathRate(){
      // Show death rates layer
      const getVal = feat => Math.log(feat.properties[this.deathRateColumn]);
      fetch(this.deathRateFilePath).then(res => res.json()).then(countries =>
      {
        const maxVal = Math.max(...countries.features.map(getVal));
        this.deathRateColorScale.domain([0, maxVal]);
        this.world
          .polygonsData(countries.features.filter(d => d.properties.ISO_A3 !== 'AQ'))
          .polygonAltitude(0.06)
          .polygonCapColor(d => this.deathRateColorScale(getVal(d)))
          .polygonSideColor(() => 'rgba(255,255,255,0.15)')
          .polygonStrokeColor(() => 'rgba(40,70,70,0.65)')
          .polygonLabel(({ properties: d }) => this.getToolTip(d, this.deathRateColumn, "Death Rate"))
          .onPolygonHover(hoverD => this.world
            .polygonAltitude(d => d === hoverD ? 0.12 : 0.06)
            .polygonCapColor(d => d === hoverD ? '#2F4F4F' : this.deathRateColorScale(getVal(d)))
          )
          .polygonsTransitionDuration(300);

      });
    },

    showInfectionRate(){
      // Show infection rate layer
      const getVal = feat => feat.properties[this.infectionColumn];

      fetch(this.infectionFilePath).then(res => res.json()).then(countries => {
        const maxVal = Math.max(...countries.features.map(getVal));
        this.infectionColorScale.domain([0, maxVal]);
        this.world.polygonsData(countries.features.filter(d => d.properties.ISO_A3 !== 'AQ'))
          .polygonAltitude(0.06)
          .polygonCapColor(feat => this.infectionColorScale(getVal(feat)))
          .polygonSideColor(() => 'rgba(255,255,255,0.15)')
          .polygonStrokeColor(() => 'rgba(40,70,70,0.65)')
          .polygonLabel(({ properties: d }) => this.getToolTip(d, this.infectionColumn, "Infection Rate"))
          .onPolygonHover(hoverD => this.world
            .polygonAltitude(d => d === hoverD ? 0.12 : 0.06)
            .polygonCapColor(d => d === hoverD ? '#2F4F4F' : this.infectionColorScale(getVal(d)))
          )
          .polygonsTransitionDuration(300);

      });
    },

    autoRotate(auto=true){
      // Add auto-rotation
      this.world.controls().autoRotate = auto;
      if(auto){
        this.world.controls().autoRotateSpeed = this.rotationSpeed;
      }

    }
  },
  mounted() {
    this.initMap();
  },
  watch:{

  }
}
</script>

<style scoped lang="scss">

</style>
