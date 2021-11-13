<template>
  <q-page class="flex flex-center">
    <div class="q-gutter-y-md" style="max-width: 600px; width:600px;">
      <q-card>
        <q-tabs v-model="tab" dense class="text-grey, shadow" active-color="primary" indicator-color="primary" align="justify" narrow-indicator>
          <q-tab name="treatment" label="People access antiretroviral therapy" />
          <q-tab name="averted" label="ART averted deaths" />
        </q-tabs>
        <q-separator />
        <q-tab-panels v-model="tab" animated keep-alive="true">
          <q-tab-panel name="treatment" id="treatmentchart" style="height: 450px">

          </q-tab-panel>
          <q-tab-panel name="averted" id="avertedchart" style="height: 450px">
          </q-tab-panel>
        </q-tab-panels>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: 'WorldARTTrend',
  data() {
    return {
      tab: 'treatment',
      years: [2000, 2005, 2010, 2015, 2016, 2017, 2018, 2019],
      num_treatment: [0.59, 2, 7.8, 17.2, 19.3, 21.5, 23.1, 25.4],

      num_treatment_high: [0.59, 2, 7.9, 17.4, 19.5, 21.7, 23.4, 25.6],
      num_treatment_diff: [0, 0, 1, 2.7, 2.9, 2.2, 1.6, 1.1],

      num_treatment_low: [0.59, 2, 6.9, 14.7, 16.6, 19.5, 21.8, 24.5],

      years2: [1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016],
      death_averted: [0, 0, 0, 0, 0, 0, 0.03, 0.08, 0.1, 0.11, 0.11, 0.13, 0.15, 0.19, 0.3, 0.55, 0.88, 1.3, 1.76, 2.03, 2.21, 2.5, 2.92, 3.21, 3.37, 3.45, 3.51],
      deaths: [0.89, 1.13, 1.4, 1.7, 2.05, 2.42, 2.8, 3.15, 3.57, 4, 4.44, 4.83, 5.19, 5.51, 5.72, 5.75, 5.62, 5.38, 5.01, 4.65, 4.35, 4.08, 3.82, 3.55, 3.31, 3.11, 2.96],
    };
  },
  methods: {
    setChart1() {
      const chartDom1 = document.getElementById('treatmentchart');
      const el = document.createElement("div");
      el.style.width = "100%";
      el.style.height = "100%";
      chartDom1.appendChild(el);

      const chart1 = echarts.init(el);

      const option1 = {
          title: {
            text: 'People Receiving ART',
            subtext: 'Number of people who hava access to ART from 2000-2019',
            left: 'center',
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'cross',
              animation: false,
              label: {
                backgroundColor: '#ccc',
                borderColor: '#aaa',
                borderWidth: 1,
                shadowBlur: 0,
                shadowOffsetX: 0,
                shadowOffsetY: 0,

                color: '#222',
              },
            },
            formatter: function (params) {
              return params[2].name + '<br />' + params[2].value.toFixed(2) + ' million';
            },
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
            max: 26,
            axisLabel: {
              formatter: function (val) {
                return val + 'million';
              },
            },
            axisPointer: {
              label: {
                formatter: function (params) {
                  return params.value.toFixed(2) + ' million';
                },
              },
            },
          },
          series: [
            {
              name: 'L',
              type: 'line',
              data: this.num_treatment_low,
              lineStyle: {
                opacity: 0,
              },
              stack: 'confidence-band',
              symbol: 'none',
            },
            {
              name: 'U',
              type: 'line',
              data: this.num_treatment_diff,
              lineStyle: {
                opacity: 0,
              },
              areaStyle: {
                color: '#279B48',
              },
              stack: 'confidence-band',
              symbol: 'none',
            },
            {
              type: 'line',
              data: this.num_treatment,
              hoverAnimation: false,
              symbolSize: 6,
              itemStyle: {
                color: '#0A171D',
              },
              showSymbol: false,
            },
          ],
        };
      chart1.setOption(option1);
    },
    setChart2() {
      const chartDom2 = document.getElementById('avertedchart');

      const el = document.createElement("div");
      el.style.width = "100%";
      el.style.height = "100%";
      chartDom2.appendChild(el);

      const chart2 = echarts.init(el);

      const option2 = {
        color: ["#868686", "#279B48"],
        title: {
          text: 'HIV/AIDS deaths and deaths averted due to ART',
          left: 'center'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#6a7985',
            },
          },
        },
        legend: {
          top: 30,
          left: 'center',
          data: ['Death Averted by ART', 'Total Death'],
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true,
        },
        xAxis: [
          {
            type: 'category',
            boundaryGap: false,
            data: this.years2,
          },
        ],
        yAxis: [
          {
            type: 'value',
          },
        ],
        series: [
          {
            name: 'Total Death',
            type: 'line',
            smooth: true,
            stack: 'death',
            label: {
              show: false,
            },
            areaStyle: {},
            emphasis: {
              focus: 'series',
            },
            data: this.deaths,
          },
          {
            name: 'Death Averted by ART',
            type: 'line',
            smooth: true,
            stack: 'death',
            areaStyle: {},
            emphasis: {
              focus: 'series',
            },
            data: this.death_averted,
          },
        ],
      };
      chart2.setOption(option2);
    },
  },
  mounted() {
    this.setChart1();
  },
  watch: {
    tab() {
      // wait for chart initialization
      setTimeout(() => {
        switch (this.tab) {
          case 'treatment':
            this.setChart1();
            break;
          case 'averted':
            this.setChart2();
            break;
        }
      }, 100);
    },
  },
};
</script>
