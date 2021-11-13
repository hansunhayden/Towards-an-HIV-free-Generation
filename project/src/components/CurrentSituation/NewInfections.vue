<template>
<!--  CHART: New HIV infections 2019 (million) -->
  <div id="newinfections" style="width:100%; height: 400px"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "NewInfections",
    data() {
    return {
      areas: [
      'Eastern and Southern Africa',
      'Asia and the Pacific',
      'Western and Central Africa',
      'Latin America',
      'The Caribbean',
      'Middle East and North Africa',
      'Eastern Europe and Central Asia',
      'Western and Central Europe and North America'
      ],
      total: [0.73,  0.3,   0.24,  0.12,   0.013,   0.02,  0.17, 0.065],
      age15: [0.66,  0.228, 0.19,  0.12,   0.012,   0.018, 0.16, 0.065],
      age14: [0.074, 0.015, 0.052, 0.0034, 0.00096, 0,     0,    0.0014]
    };
  },
  async mounted() {
    var chartDom = document.getElementById('newinfections');
    var myChart = echarts.init(chartDom);
    var option;

    option = {
      color: ["#D8D085", "#00A296"],
      title: {
          text: 'New HIV infections 2019 (million)',
          subtext: 'from UNAIDS fact sheet 2021 \n *0 represents estimates for children are not published because of the small numbers.',
          left: "center",
          top: "top",
      },
      tooltip: {
          trigger: 'axis',
          axisPointer: {            // Use axis to trigger tooltip
              type: 'shadow'        // 'shadow' as default; can also be 'line' or 'shadow'
          }
      },
      legend: {
          data: ['Aged 0–14', 'Aged 15+'],
          left: "right",
          top: 'top',
          orient: 'vertical'
      },
      grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
      },
      xAxis: {
          type: 'value'
      },
      yAxis: {
          type: 'category',
          data: this.areas
      },
      series: [
        {
            name: 'Aged 0–14',
            type: 'bar',
            stack: 'total',
            label: {
                show: false
            },
            emphasis: {
                focus: 'series'
            },
            data: this.age14
        },
        {
            name: 'Aged 15+',
            type: 'bar',
            stack: 'total',
            label: {
                show: false
            },
            emphasis: {
                focus: 'series'
            },
            data: this.age15
        }
      ]
    };

    option && myChart.setOption(option);
  }
}
</script>

<style  scoped>
</style>
