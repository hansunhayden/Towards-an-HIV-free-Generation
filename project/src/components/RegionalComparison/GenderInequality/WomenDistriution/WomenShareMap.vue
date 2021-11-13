<template>
<!--  MAP: Global 2D map to show share of women-->
  <div>
    <div id="map-women" class="basemap"/>

    <!-- Legend -->
    <div class="legend-container">
      <div class="legend" id="legend">
        <h2 class="text-body1 text-weight-bold">Share of women among population living with HIV</h2>
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
  name: 'WomenShareMap',
  data: function () {
    return {
      map: null,
      input: 2017,
      breaks: [
        [0, '#08BAAD'],
        [20, '#6dc6a6'],
        [40, '#9fd0a8'],
        [45,'#c6dbb4'],
        [50,'#f8dcbc'],
        [55,'#f3ae7d'],
        [60,'#f19563'],
        [80, '#EF7A4E'],
        [100, '#EF7A4E'],
      ],
      current_year: 2017
    };
  },
  methods: {
    initMap() {
      this.map = new mapboxgl.Map({
        container: 'map-women',
        style: 'mapbox://styles/jennyli/ckohe8fg94l9217olugjwrycx',
        minZoom: 1.5,
        zoom: 1.5,
        maxZoom: 3,
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
        map.addSource('womenShare', {
          type: 'vector',
          url: 'mapbox://jennyli.cw16npzi',
        });

        map.addLayer({
          id: 'layer_id',
          type: 'fill',
          source: 'womenShare',
          'source-layer': 'share-of-women-among-the-popu-9w0raa',
          paint: {
            'fill-color': {
              property: this.current_year +'_women_share',
              type: 'interval',
              stops: this.breaks,
            },
            'fill-opacity': 1,
            'fill-outline-color':'rgba(0,0,0,0)',
          },
        },firstSymbolId);

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
            let line2 = '<p> Share of women ' +this.current_year+': '+ (propObj[this.current_year +'_women_share']).toFixed(2) + '%</p>';
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
      // Change the year of data to show
      this.input = e;
      this.current_year = e;
      this.map.setPaintProperty( 'layer_id', 'fill-color', {
        property: this.current_year +'_women_share',
        type: 'interval',
        stops: this.breaks});
    },
    setLegend() {
      // Draw legend
      const e = this.$refs['cd-legend'];
      let bar_html = '';
      let upper_bar_html = '';
      let legendLabels = [];
      this.breaks.forEach((e,i)=> legendLabels.push(e[0]));

      var acc_width = 0;
      for (let i=0; i<legendLabels.length; i++) {
        let label = legendLabels[i];
        let width = (legendLabels[i]-acc_width)*4;
        let color = '';
        if(label===100){
          label+="%";
        }
        if(label!==0){
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

      e.innerHTML = upper_bar_html+`<br/>`+bar_html;
    },
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

/* Legend Container */
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
