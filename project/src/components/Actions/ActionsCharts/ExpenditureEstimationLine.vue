<template>
<div ref="chart" style="height:300px; width:100%"></div>
  <div class="text-body2 q-ml-md">Estimated resources for prevention and treatment of HIV in low-to-middle income countries of a given region, measured in constant 2016 US$. Also shown are UNAIDS estimates of annual resource needs to meet fast-track HIV targets by 2030.</div>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: "ExpenditureEstimationLine",
  data(){
    return {
      chartOptions: null,
      years:[],
      fundData:[10.00,11.99,15.28,15.36,15.58,17.37,18.10,19.14,18.77,18.68,19.12,],
      fundEstimate:[,,,,,,,,,,,,25.72,26.04,26.17,25.27,25.32,25.40,25.49,25.58,25.24,24.59,24.91,24.26,23.93]
    }
  },
    mounted(){
      this.initChart();
    },
  methods:{
    initChart(){
      this.years = this.range(2006,2030);
      this.chartOptions = {
        title: {
          text: 'HIV Funding and Estimated Future Requirements, 2006 to 2030',
          left: 'left',
          subtextStyle:{
            // fontSize: 16,
            height:500,
          },
        },
        tooltip: {
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true,
        },
        xAxis: {
          type: 'category',
          data: this.years,
          boundaryGap: false,
        },
        yAxis: {
          max: 30,
          axisLabel: {
            formatter: function (val) {
              return '$'+ val + ' billion';
            },
          },
          axisPointer: {
            label: {
              formatter: function (params) {
                return '$'+params.value.toFixed(2) + ' billion';
              },
            },
          },
        },
        series: [
          {
            name: 'Current HIV resource funding',
            type: 'line',
            data: this.fundData,
            areaStyle: {},
            color:'#868686'
          },
          {
            name: 'Estimated future requirements',
            type: 'line',
            data: this.fundEstimate,
            areaStyle: {},
            color:'#279B48'
          },
        ],
      };
      this.myChart = echarts.init(this.$refs["chart"]);
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    },
    range(start, end) {
      return Array(end - start + 1).fill().map((_, idx) => start + idx)
    },
  }
}
</script>

<style scoped>

</style>
