<template>
<!--  CHART: Line chart to show time series data in regional comparison-->
  <div class="q-mb-lg items-center">
    <div class="q-mb-xs" ref="chart" style="height:416px"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: "TimeseriesLineChart",
  props: ["timeseriesData","timeseriesChartinfo","baselineData","title","baselineLegend"],
  data() {
    return{
      xAxisData: this.range(1990,2017),
      chartOptions:  {},
      baselineSeries: {},
      dataSeries: {}
    }
  },
  mounted() {
    this.initChart();
  },
  methods:{
    initChart: function () {
      this.myChart = echarts.init(this.$refs["chart"]);
      this.baselineSeries = {
        name: this.baselineLegend,
        data: this.baselineData,
        type: 'line',
        smooth: true,
        color: "#EF7A4E",
      };
      this.dataSeries = {
        type: 'line',
        smooth: true,
        color: "#08baad",
      };
      this.chartOptions={
        title:{
          text: this.title,
          subtext:"Click the map and see the time-series difference in the line chart.",
          left: 45,
        },
        legend:{
          left: 100,
          bottom:10,
          orient:'horizontal',
          data: [this.baselineLegend,""]
        },
        tooltip: {
          trigger: 'axis'
        },
        xAxis: {
          type: 'category',
            data: this.xAxisData,
        },
        yAxis: {
          type: 'value'
        },
        series: [this.baselineSeries, this.dataSeries],
      };
      this.chartOptions && this.myChart.setOption(this.chartOptions);

    },
    range: function(start, end) {
      return Array(end - start + 1).fill().map((_, idx) => start + idx)
    },
  },
  watch:{
    timeseriesData: function(val){
      // Show the data from the picked country
      this.dataSeries.data = val;
      this.dataSeries.name = this.timeseriesChartinfo;
      this.chartOptions.series = [this.baselineSeries, this.dataSeries];
      this.chartOptions.legend.data[1] = this.timeseriesChartinfo;
      this.chartOptions && this.myChart.setOption(this.chartOptions);

    },
    baselineData: function(val){
      // Show regional average data
      this.baselineSeries.data = val;
      this.baselineSeries.name = this.baselineLegend;
      this.chartOptions.series = [this.baselineSeries, this.dataSeries];
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    },
    title: function(val){
      // Change title
      this.chartOptions.title.text = val;
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    }
  }
}
</script>

<style scoped>

</style>
