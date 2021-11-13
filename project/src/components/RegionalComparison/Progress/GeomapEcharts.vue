<template>
<!--  Map for Western Europe and Sub-Saharan Africa-->
  <div style="height:500px; width:100%" class="column">
      <div ref="geomap" style="height:100%; width:100%"/>
  </div>

</template>

<script>
import * as echarts from "echarts";

export default {
  name: "GeomapEcharts",
  props: ["region","geoJson","deathRateJson","deathShareJson"],
  data(){
    return{
      myChart: null,
      chartOptions: null,
      deathShareColumn: '2017_infection_rate',
      deathRateColumn: '2017_death_rate',
      basemapJson: this.geoJson,
      isActive: false, // Show death rate first
      val_min:0,
      val_max:0,
      mapData: [],
      iso2name: [],
      selectedContent: {data:"", series:""},
      selected: false,
      changedLayer: false,
      deathRateSeriesName:'HIV Death Rates',
      deathShareSeriesName:'New Infections of HIV/AIDS',

      mapCenter: [],
      mapLevel: 1.1,
    }
  },

  mounted() {

    this.initChart();
  },
  watch: {
    isActive: function(val){
      this.$emit('isActive', val);
    }

  },

  methods:{
    initChart: function () {
      // Map center
      if(this.region==="Western Europe"){
        this.mapCenter = [6.35,49]
        this.mapLevel = 6
      }else if(this.region==="Sub-Saharan Africa"){
        this.mapCenter = [20,0]
      }
      this.mapRegister();

      this.getData(this.deathRateJson, this.deathRateColumn);
      this.showDeathRate(this.deathRateJson);
      // Add map onClick Listener, get time series data of the clicked country
      let self = this;
      this.myChart.on("click", function(params){
        if(params.data){
          if(params.data.name===self.selectedContent.data) {
            self.$emit("dataChange",
              [],
              self.selectedContent.series,
              ""
            );
            self.selected = false;
            self.selectedContent.data = "";
            self.selectedContent.series = "";
          }else{
            self.selected = true;
            self.selectedContent.data = params.data.name;
            self.selectedContent.series = params.seriesName;
          }
          if(self.selected){
            self.changeSelection();
          }
        }

      });



    },

    getData: function (jsondata, column) {
      this.mapData = [];
      this.basemapJson['features'].forEach(feat =>{
        let match_country = jsondata.filter(value => value.ISO_A3===feat.properties.name);
        if(match_country.length>0){
          this.mapData.push({name: feat.properties.name, value: match_country[0][column]});
        }

      });
      this.val_max = Math.max(...jsondata.map(item=>item[column]));
      this.val_min = Math.min(...jsondata.map(item=>item[column]));
    },

    mapRegister: function () {
      // Register Map
      this.myChart = echarts.init(this.$refs["geomap"]);
      this.myChart.showLoading();
      echarts.registerMap('Sub-Saharan Africa', this.basemapJson);
    },

    countryCodeToName: function(jsondata, country_code){
      // Map country code to country name
      let country_name = jsondata.filter(value => value.ISO_A3===country_code)[0]['Entity'];
      return country_name;
    },

    changeSelection: function(){
      // When picked country polygon changed, change the data shown in line chart
      let series = this.selectedContent.series;
      let country_iso = this.selectedContent.data;
      let timeseriesList = [];
      if(series===this.deathShareSeriesName){
        let selectedCountry = this.deathShareJson.filter(value => value.ISO_A3===country_iso)[0];
        for(let y=1990; y<2018; y+=1){
          timeseriesList.push(selectedCountry[y+this.deathShareColumn.slice(4)]);
        }
      }else if(series===this.deathRateSeriesName){
        let selectedCountry = this.deathRateJson.filter(value => value.ISO_A3===country_iso)[0];
        for(let y=1990; y<2018; y+=1){
          timeseriesList.push(selectedCountry[y+this.deathRateColumn.slice(4)]);
        }
      }
      this.$emit("dataChange",
        timeseriesList,
        this.selectedContent.series,
        this.countryCodeToName(this.deathShareJson, country_iso)
      );
    },

    showDeathRate(jsondata){
      this.myChart.hideLoading();
      this.chartOptions = {
        title: {
          text: this.deathRateSeriesName+' in '+this.region+', 2017',
          subtext: 'The number of deaths from HIV/AIDS per 100,000 people.',
          left: 'left'
        },
        tooltip: {
          trigger: 'item',
          showDelay: 0,
          transitionDuration: 0.2,
          formatter: function (params) {
            var country_name = jsondata.filter(value => value.ISO_A3===params.name)[0]['Entity']
            return params.seriesName + '<br/><b>' + country_name + ':</b> ' + params.value.toFixed(2);
          }
        },
        visualMap: {
          left: 'left',
          min: this.val_min,
          max: this.val_max,
          inRange: {
            color:['#08baad','#7DC7C0','#f1f1e1','#F9C1A5','#EF7A4E']
          },
          text: ['High', 'Low'],
          calculable: true
        },
        series: [
          {
            name: this.deathRateSeriesName,
            type: 'map',
            roam: true,
            map: 'Sub-Saharan Africa',
            zoom: this.mapLevel,
            scaleLimit:{
              min:1,
              max:this.mapLevel+1,
            },
            center: this.mapCenter,
            emphasis: {
              label: {
                show: true,
                position:"inside",
                color: "#000",
                fontWeight: "bold"
              },
              itemStyle: {
                areaColor: "#b6ada7"
              }
            },
            select:{
              label: {
                show: true,
                position:"inside",
                color: "#000",
                fontWeight: "bold"
              },
              itemStyle: {
                borderColor: "#FFFFFF",
                borderWidth: 5,
                shadowColor:"#FFFFFF",
                shadowOffsetX: 1,
                shadowOffsetY: 1,
                opacity:1,
              }
            },
            data: this.mapData,
            itemStyle: {
              borderColor: "#FFFFFF",
              borderWidth: 1.5,
            },
          }
        ],
      };
      this.myChart.setOption(this.chartOptions);

      this.chartOptions && this.myChart.setOption(this.chartOptions);
    },

    showDeathShare(jsondata){

      this.myChart.hideLoading();
      this.chartOptions = {
        title: {
          text: this.deathShareSeriesName+' in '+this.region+', 2017',
          subtext: 'The share of new infections of HIV/AIDS among all population per country.',
          left: 'left'
        },
        tooltip: {
          trigger: 'item',
          showDelay: 0,
          transitionDuration: 0.2,
          formatter: function (params) {
            var country_name = jsondata.filter(value => value.ISO_A3===params.name)[0]['Entity']
            return params.seriesName + '<br/>' + country_name + ': ' + params.value.toFixed(2)+'%';
          }
        },
        visualMap: {
          left: 'left',
          min: this.val_min,
          max: this.val_max,
          inRange: {
            color:['#08baad','#7DC7C0','#f1f1e1','#F9C1A5','#EF7A4E']
          },
          text: ['High', 'Low'],
          calculable: true
        },

        series: [
          {
            name: this.deathShareSeriesName,
            type: 'map',
            roam: true,
            map: 'Sub-Saharan Africa',
            zoom: this.mapLevel,
            center: this.mapCenter,
            emphasis: {
              label: {
                show: true,
                position:"inside",
                color: "#000",
                fontWeight: "bold"
              },
              itemStyle: {
                areaColor: "#b6ada7"
              }
            },
            select:{
              label: {
                show: true,
                position:"inside",
                color: "#000",
                fontWeight: "bold"
              },
              itemStyle: {
                borderColor: "#FFFFFF",
                borderWidth: 5,
                shadowColor:"#FFFFFF",
                shadowOffsetX: 1,
                shadowOffsetY: 1,
                opacity:1,
              }
            },
            data: this.mapData,
            itemStyle: {
              borderColor: "#FFFFFF",
              borderWidth: 1.5,

            },


          }
        ],

      };
      this.myChart.setOption(this.chartOptions);

      this.chartOptions && this.myChart.setOption(this.chartOptions);
    },

    toggle() {
      // When toggle button clicked, show death rate or infection rate map
      this.isActive = !this.isActive;
      let title = "";

      if (this.isActive){
        this.getData(this.deathShareJson, this.deathShareColumn);
        this.showDeathShare(this.deathShareJson);
        title = this.deathShareSeriesName;
      }else{
        this.getData(this.deathRateJson, this.deathRateColumn);
        this.showDeathRate(this.deathRateJson);
        title = this.deathRateSeriesName;
      }
      this.$emit("titleChange", title);
      this.selectedContent.series = title;
      if(this.selected){
        this.changeSelection();
      }
    },
  }
}
</script>

<style scoped>
.toggle-button-container {

  z-index: 2;
  border: 1px solid;
}
</style>
