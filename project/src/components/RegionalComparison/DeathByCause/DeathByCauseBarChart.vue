<template>
  <div ref="chart" style="height:400px; width:100%;">
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "DeathByCauseBarChart",
  props:['series-data','name','categories'],
  data(){
    return{
      min:0,
      max:0,
      chartOptions:{
        title: {
          text: this.name+" - Number of Deaths By Cause",
          subtext: 'Top 20 causes to death, 2017',
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        grid: {
          left:210,
        },
        // toolbox: {
        //   show: true,
        //   feature: {
        //     saveAsImage: {}
        //   }
        // },
        xAxis: {
          type: 'value',
          name: 'K',
          axisLabel:{
            formatter: function(val){
              return (val/1000.0).toFixed(0)
            }
          }

        },
        yAxis: {
          type: 'category',
          inverse: true,
          data: this.categories,
          axisLabel:{
            width: 200,
            margin:10,
            overflow: 'truncate',
            ellipsis:'...',
            textStyle: {
              fontSize: 14,
            },

          }
        },
        visualMap: {
          orient: 'horizontal',
          left: 'center',
          min: 0,
          max: 0,
          text: ['High', 'Low'],
          // Map the score column to color
          dimension: 0,
          inRange: {
            color: ['#65B581', '#FFCE34', '#FD665F']
          }
        },
        series: [
          {
            name: 'Top 20 death causes',
            type: 'bar',
            data: this.seriesData,
            // label: seriesLabel,
          },
        ]

      },

    }
  },
  methods:{
    initChart(){
      this.min = Math.min(...this.seriesData);
      this.max = Math.max(...this.seriesData);
      this.chartOptions.visualMap.min = this.min;
      this.chartOptions.visualMap.max = this.max;
      this.myChart = echarts.init(this.$refs["chart"]);
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    }
  },
  mounted(){
    this.initChart();
  },
}
</script>

<style scoped>

</style>
