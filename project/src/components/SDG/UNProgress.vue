<template>
<!--  CHART: Progress of UNAIDS -->
  <div>
    <div id="un_progress" style="height:500px; margin-bottom:0px; padding-bottom:0px;"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "UNProgress",
  data() {
    return {
      source: [
        ['Year', 'Infections', 'Deaths'],
        ['2000', 2.4, 1.4],
        ['2005', 2.7, 1.7],
        ['2010', 2.1, 1.1],
        ['2015', 1.9, 0.83],
        ['2016', 1.8, 0.8],
        ['2017', 1.8, 0.76],
        ['2018', 1.7, 0.73],
        ['2019', 1.7, 0.69]
      ]
    }
  },
  mounted() {
    var chartDom = document.getElementById('un_progress');
    var myChart = echarts.init(chartDom);
    var option;

    option = {
      color: ['#006E66', '#7DC4CB'],
      legend: {
        left: 'right'
      },
      title: {
        text: 'UN Progress in HIV Prevention and Treatment',
        subtext: 'Number of HIV infections and relate deaths from 2000-2019',
        left: 'left'
      },
      tooltip: {
        formatter: function (params) {
          //console.log(params.data[1])
          return params.data[0] + '<br />Infections: ' + params.data[1].toFixed(2) + ' million' + '<br />Deaths: ' + params.data[2].toFixed(2) + ' million';
        },
      },
      dataset: {
        source: this.source
      },
      xAxis: {type: 'category'},
      yAxis: {
        axisLabel: {
          formatter: function (val) {
            return val + ' million';
          },
        }
      },
      series: [
          {type: 'bar'},
          {type: 'bar'}
        ]
    };
    option && myChart.setOption(option);
  },
}
</script>

<style  scoped>

</style>
