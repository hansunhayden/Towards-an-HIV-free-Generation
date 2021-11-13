<template>
<!--  MAP: Global 2D map to show number of children living with HIV-->
  <div>
    <div id="map-childHIV" class="basemap"></div>
    <!-- Legend -->
    <div class="legend-container">
      <div class="legend" id="legend">
        <h2 class="text-body1 text-weight-bold">The number of children living with HIV per country</h2>
        <hr />
        <div class="text-body2 slider">
          <q-slider
            v-model="current_year"
            markers
            :min="1990"
            :max="2017"
            label
            label-always
            @change="slider"
            color="orange"
          />
        </div>
        <hr />
        <div class="legend" ref="cd-legend"></div>
      </div>
    </div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl';
mapboxgl.accessToken = 'pk.eyJ1IjoiamVubnlsaSIsImEiOiJja254NWVoZTMwNjYxMndyeHVyYnlqbjJuIn0.Wgh8N0qRAw1ax8myJ5TdOQ';

export default {
  name: 'ChildrenHIVMap',
  data: function () {
    return {
      map: null,
      input: 2017,
      breaks: [
        [0, 'rgb(255,245,240)'],
        [2500, 'rgb(254,224,210)'],
        [5000, 'rgb(252,187,161)'],
        [10000,'rgb(252,146,114)'],
        [25000,'rgb(251,106,74)'],
        [50000,'rgb(239,59,44)'],
        [100000,'rgb(203,24,29)'],
        [250000, 'rgb(165,15,21)'],
        [500000, 'rgb(103,0,13)'],
      ],
      current_year: 2017
    };
  },
  methods: {
    initMap() {
      this.map = new mapboxgl.Map({
        container: 'map-childHIV',
        style: 'mapbox://styles/jennyli/ckohe8fg94l9217olugjwrycx',
        zoom: 1.5,
        maxZoom: 3,
        minZoom: 1.5,
        center: [20, 15],
      });
    },
    setMap() {
      const map = this.map;

      map.on('load', () => {
        let layers = map.getStyle().layers;
        // Find the index of the first symbol layer in the map style
        let firstSymbolId;
        for (let i = 0; i < layers.length; i++) {
          if (layers[i].type === 'symbol') {
            firstSymbolId = layers[i].id;
            break;
          }
        }
        map.addSource('childHIV', {
          type: 'vector',
          url: 'mapbox://jennyli.3dnynzwc',
        });

        map.addLayer({
          id: 'layer_id',
          type: 'fill',
          source: 'childHIV',
          'source-layer': 'children-living-with-hiv-bo7oj2',
          paint: {
            'fill-color': {
              property: this.current_year +'_child',
              type: 'interval',
              stops: this.breaks,
            },
            'fill-opacity': 1,
            'fill-outline-color':'rgba(0,0,0,0)',
          },
        },
          firstSymbolId
        );


        map.on('mouseleave', 'layer_id', function () {
          map.getCanvas().style.cursor = '';
        });


        map.on('mouseenter', 'layer_id', function () {
          map.getCanvas().style.cursor = 'pointer';
        });

        let popup = new mapboxgl.Popup({
          closeButton: false,
          closeOnClick: true,
        });

        // when user click layer, show info window
        map.on('click', 'layer_id', (e) => {
          if (e.features.length > 0) {
            let propObj = e.features[0].properties;
            let line1 = '<strong>' + propObj['NAME_LONG'] + '</strong><br/>';
            let line2 = '<p> Children living with HIV '+this.current_year+': ' + this.getFormatValue(propObj[this.current_year +'_child']) + 'K</p>';
            popup.remove();
            popup
              .setLngLat(e.lngLat)
              .setHTML(line1 + line2)
              .addTo(map);
          }
        });


      });
    },
    slider(e) {
      // Update data of the year to show
      this.input = e;
      this.current_year = e;
      this.map.setPaintProperty( 'layer_id', 'fill-color', {
        property: this.current_year +'_child',
        type: 'interval',
        stops: this.breaks});
    },
    setLegend() {
      // Draw legend
      const e = this.$refs['cd-legend'];
      let bar_html = '';
      let upper_bar_html = '';
      let lower_bar_html = '';

      let legendLabels = [];
      this.breaks.forEach((e,i)=> legendLabels.push(e[0]));

      var acc_width = 0;
      for (let i=0; i<legendLabels.length; i++) {
        let label = this.getFormatValue(legendLabels[i]);
        let width = (legendLabels[i]-acc_width)/1500;
        let color = '';
        if(i===legendLabels.length-1){
          label+="K";
        }else if(i>0 && i<5){
          label="";
        }
        if(i!==0){
          color = this.breaks[i-1][1];
        }
        bar_html += `<span style=" display: inline-block;
                                    width: ${width}px;
                                    height: 15px;
                                    margin-right: 1px;
                                    margin-left: 0;
                                    background:${color}"></span>`;

        upper_bar_html += `<span style=" display: inline-block;
                                          width: ${width}px;
                                          height: 15px;
                                          margin-right: 1px;
                                          margin-left: 0;
                                          text-align: right;
                                          ">${label}</span>`;
        acc_width = legendLabels[i];

      }

      e.innerHTML = `<p>`+upper_bar_html+`<br/>`+bar_html+`</p>`;
    },

    getFormatValue(d, digit=0){
      return (d/1000).toFixed(digit);
    }
  },
  mounted() {
    this.initMap();
    this.setMap();
    this.setLegend();
  },
};
</script>

<style scoped>

.basemap {
  width: 100%;
  height: 75vh;
}

/* legend test */
.legend-container {
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 20px 20px;
  z-index: 9;
  max-width: 500px;

}


/*Mapbox Legend */
.legend {
  font: 12px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
  background-color: rgba(255,255,255,0.4);
  padding: 10px;
  width: 100%;
  margin: auto;
  z-index: 10;
  text-align: center;
}

/* Legend title */
.legend h2 {
  padding-top: 8px;
  margin: 0;
  text-align: center;
}

.legend hr {
  color: #123455;
  border: 0;
  border-top: 1px solid #ccc;
  padding: 0;
  margin-top: 5px;
  margin-bottom: 5px;
}
.slider {
  margin: auto;
  text-align: center;
  width:75%;
  padding-top:15px;
  margin-bottom:0;
}
</style>

