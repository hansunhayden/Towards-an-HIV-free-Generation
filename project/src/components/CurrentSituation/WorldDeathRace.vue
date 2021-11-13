<template>
<!--  CHART: Race between countries on HIV-related death -->
  <div style="width: 100%">
    <div id="death_rate_chart_race" style="width: 100%; height: 400px"></div>
    <div>
      <q-btn class="btn" round :icon="icon" @click="play" />
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import death_rate_top10 from '../../../public/data/death_rate_top10';

let myChart = null;
export default {
  name: 'WorldDeathRace',
  data: () => {
    return {
      icon: 'play_arrow',
      option: null,
      updateFrequency: 2000,
      clock: 0,
      years: [1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017],
    };
  },
  methods: {
    play() {
      if (this.icon === 'play_arrow') {
        this.icon = 'replay';
      }

      clearInterval(this.clock);

      let clockCount = 1;
      this.updateYear(this.years[clockCount++]);
      this.clock = setInterval(() => {
        this.updateYear(this.years[clockCount++]);
        if (clockCount == this.years.length) {
          clearInterval(this.clock);
        }
      }, this.updateFrequency);
    },
    updateYear(year) {
      this.option.series[0].data = death_rate_top10.filter((d) => {
        return d[1] == year;
      });
      this.option.graphic.elements[0].style.text = year;
      myChart.setOption(this.option);
    },
  },
  mounted() {
    myChart = echarts.init(document.getElementById('death_rate_chart_race'));
    let cacheColors = { count: 0 };
    let countryColors = ["#1AAA9A", "#6EC9BF", "#69A5A4", "#1AAA9A", "#6EC9BF", "#69A5A4"];
    //default
    this.option = {
      title: {
        text: ' HIV Death Rate Highest 10 Countries',
        subtext: 'from 1990 - 2017',
        left: 'left',
        top: 0,
      },
      grid: {
        top: 40,
        bottom: 30,
        left: 210,
        right: 80,
      },
      xAxis: {
        max: (e) => {
          Math.round(e.max);
        },
        label: {
          formatter: (n) => {
            return Math.round(n);
          },
        },
      },
      yAxis: {
        type: 'category',
        inverse: true,
        max: 9,
        label: {
          formatter: (n) => {
            return Math.round(n);
          },
        },
        axisLabel: {
          show: true,
          textStyle: {
            fontSize: 14,
          },
          rich: {
            flag: {
              fontSize: 25,
              padding: 5,
            },
          },
        },
        animationDuration: 600,
        animationDurationUpdate: 600,
      },
      visualMap: {
        orient: 'horizontal',
        top: 0,
        left: 'right',
        min: 0,
        max: 70,
        text: ['70%', '0%'],
        // Map the score column to color
        dimension: 2,
        inRange: {
            color: ['#7DC7C0', '#E1DFA8', '#EF7A4E']
        }
      },
      series: [
        {
          realtimeSort: true,
          seriesLayoutBy: 'column',
          type: 'bar',
          itemStyle: {
            color: (param) => {
              if (!cacheColors[param.value[0]]) {
                cacheColors[param.value[0]] = countryColors[cacheColors.count%6];
                cacheColors.count++;
              }
              return cacheColors[param.value[0]];
            },
          },
          data: death_rate_top10.slice(0, 10),
          encode: {
            x: 2,
            y: 0,
          },
          label: {
            show: true,
            precision: 1,
            position: 'right',
            valueAnimation: true,
            fontFamily: 'monospace',
            formatter: (d) => {
              return Math.round(d.data[2]) + '%'
            },
          },
        },
      ],
      animationDuration: 0,
      animationDurationUpdate: this.updateFrequency,
      animationEasing: 'linear',
      animationEasingUpdate: 'linear',
      graphic: {
        elements: [
          {
            type: 'text',
            right: 70,
            bottom: 20,
            style: {
              text: this.years[0],
              font: 'bolder 80px monospace',
              fill: 'rgba(100, 100, 100, 0.25)',
            },
            z: 100,
          },
        ],
      },
    };
    myChart.setOption(this.option);
  },
};
</script>
<style>
.btn {
  float: right;
  position: relative;
  bottom: 130px;
  right: 130px;
  z-index: 999;
  background-color: #fff;
  color: #00000060;
}
.btn:hover {
  color: #000000;
}
</style>
