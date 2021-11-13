<template>
  <div ref="chart" style="height:350px"></div>

</template>

<script>
import * as echarts from 'echarts';
import {expenditure_flow, data, test} from "assets/json/expenditure";
export default {
name: "ExpenditureSunburst",
  data(){
    return{
      chartOptions: {
        title: {
          text: 'Funding Resources of UNAIDS',
          subtext: 'Joint United Nations Programme on HIV/AIDS in 2019 (Unit: USD)',
          left:10,
          bottom:0,
        },
        tooltip: {
          trigger: 'item',
          triggerOn: 'mousemove'
        },
        series: [
          {
            name:"Joint United Nations Programme on HIV/AIDS in 2019 (Unit: USD)",
            type: 'sankey',
            data: expenditure_flow.nodes,
            links: expenditure_flow.links,
            nodeWidth: 25,
            emphasis: {
              focus: 'adjacency'
            },
            levels: [{
              depth: 0,
              itemStyle: {
                color: '#D8D085'
              },
              lineStyle: {
                color: '#b8c9ec',
                opacity: 0.6
              }
            }, {
              depth: 1,
              itemStyle: {
                color: '#F9C1A5'
              },
              lineStyle: {
                color: 'source',
                opacity: 0.6
              }
            }, ],
            lineStyle: {
              curveness: 0.5
            }
          }
        ]
      },
      myChart: null
    }
  },
  methods:{
    initChart(){
      this.myChart = echarts.init(this.$refs.chart);
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    }
  },
  mounted() {
    this.initChart();
  },
}
</script>

<style scoped>

</style>
