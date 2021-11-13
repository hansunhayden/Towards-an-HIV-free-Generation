<template>
<!--  CHART: Pictorial bar to show women share-->
  <div ref="chart" style="height:200px; width:100%;"></div>
</template>

<script>
import * as echarts from 'echarts';

var image = 'https://image.flaticon.com/icons/png/512/2922/2922561.png'

var maxData = 100;

export default {
  name: "WomenSharePicutreBar",
  props:[],
  data(){
    return{
      myChart: null,
      chartOptions: {
        title:{
          text:'Share of Women among people living with HIV/AIDS in 2019',
          subtext:''
        },
        tooltip:{
          formatter: function(params){
            let seriesName = params.name;
            let html = seriesName + '<br/> Women: '+params.value+'% / Men: '+(maxData-params.value)+'%';
            return html;
          }
        },
        xAxis: {
          max: 100,
          splitLine: {show: false},
          offset: 0,
          axisLine: {
            lineStyle: {
              color: '#999'
            }
          },
          axisLabel: {
            margin: 10
          }
        },
        color:['#bb0004', '#FFD48A'],
        yAxis: {
          data: ['Sub-Saharan Africa','Western Europe'],
          inverse: true,
          axisTick: {show: false},
          axisLine: {show: false},
          axisLabel: {
            margin: 20,
            color: '#474747',
            fontSize: 16
          }
        },
        grid: {
          top: 'center',
          height: 200,
          left: 200,
          right: 100
        },
        series: [{
          // current data
          type: 'pictorialBar',
          symbol: 'image://'+image,
          symbolRepeat: 'fixed',
          symbolMargin: '10%',
          symbolClip: true,
          symbolSize: 30,
          symbolBoundingData: maxData,
          data: [60,22],
          z: 10
        }, {
          // full data
          type: 'pictorialBar',
          itemStyle: {
            normal: {
              opacity: 0.5
            }
          },
          label: {
            show: true,
            formatter: function (params) {
              return params.value.toFixed(1) + '% ';
            },
            position: 'right',
            offset: [1, 0],
            color: '#474747',
            fontSize: 16
          },
          animationDuration: 0,
          symbolRepeat: 'fixed',
          symbolMargin: '10%',
          symbol: 'image://'+image,
          symbolSize: 30,
          symbolBoundingData: maxData,
          data: [60,22],
          z: 5
        }]
    }
  }},
  mounted(){
    this.initChart()
  },
  methods:{
    initChart(){
      this.myChart = echarts.init(this.$refs["chart"]);
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    }
  }

}
</script>

<style scoped>

</style>
