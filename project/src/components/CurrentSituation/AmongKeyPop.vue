<template>
<!--  CHART: Share of new HIV infections worldwide in 2019, by key population -->
  <div>
    <div id="among_key_populations" style="width: 100%; height: 400px"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "AmongKeyPop",
  data() {
    return {
      key_pop: [
        {name: 'Clients of sex workers \n and other sexual partners \n of key populations', value: 19},
        {name: 'Sex workers', value: 8},
        {name: 'Gay men and other men \n who have sex with men', value: 23},
        {name:'Transgender women', value: 2},
        {name: 'People who inject drugs', value: 10},
        {name: 'Rest', value: 38},

      ]
    }
  },
  mounted() {
    var chartDom = document.getElementById("among_key_populations");
    var myChart = echarts.init(chartDom);
    var option;

    option = {

      title: {
          text: 'Share of new HIV infections worldwide in 2019, by key population',
          subtext: 'from UNAIDS data 2020',
          left: "center",
          top: "top",
      },

      tooltip: {
          trigger: 'item',
          formatter: function (params) {
            return "Group: " + params.data.name + "<br /> Percentage: " + params.value + "%";
          },
      },

      visualMap: {
          show: false,
          min: 0,
          max: 40,
          inRange: {
              colorLightness: [0, 0.4]
          }
      },

      series: [
          {
              name: '访问来源',
              type: 'pie',
              radius: '70%',
              center: ['50%', '50%'],
              data: this.key_pop.sort(function (a, b) { return a.value - b.value; }),
              roseType: 'radius',
              label: {
                  color: '#5a5a5a'
              },
              labelLine: {
                  lineStyle: {
                      color: '#5a5a5a'
                  },
                  smooth: 0.2,
                  length: 10,
                  length2: 20
              },
              itemStyle: {
                  color: "#00A296",
                  shadowBlur: 50,
                  shadowColor: 'rgba(0, 0, 0, 0.5)'
              },

              animationType: 'scale',
              animationEasing: 'elasticOut',
              animationDelay: function (idx) {
                  return Math.random() * 100;
              }
          }
      ]
    };

    option && myChart.setOption(option);

  },
}
</script>

<style  scoped>

</style>
