<template>
<div class="q-ma-lg items-center">
  <div class="q-mb-xs text-center text-h6 ">{{name}}</div>
  <div class="q-mb-xs" ref="chart" style="height:300px"></div>
</div>
</template>

<script>
import * as echarts from 'echarts';
import {colorcode} from "assets/json/deathByCause";

export default {
  name: "DeathByCausePieChart",
  props:["data","name"],
  data() {
    return{
      top_num: 10,
      unprocess_data: this.data,
      chart_data: null,
      myChart: null,
      color_list: [],
      chartOptions: {
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {d}%'
        },
        legend: {
          show: false,
          top: '5%',
          left: 'center'
        },
        series: [
          {
            name: this.name,
            type: 'pie',
            radius: ['55%', '95%'],
            selectedOffset: 10,
            selectedMode: 'single',
            avoidLabelOverlap: false,
            itemStyle: {
              borderRadius: 0,
              // borderColor: '#fff',
              borderWidth: 0
            },
            label: {
              show: false,
              position: 'center',
              width: 150,
              overflow: 'break',
              formatter:'{b}\n{d}%',
            },
            emphasis: {
              label: {
                show: true,
                fontSize: '17',
                fontWeight: 'bold',
                width: 150,
              },
              focus:'self',
              blurScope: 'global'
            },
            data: [],
            color:['#27727b','#c1232b','#fcce10','#e87c25','#d7504b','#b5c334','#fe8463','#9bca63','#fad860','#f3a43b','#60c0dd','#c6e579','#f4e001','#f0805a','#26c0c0','#9bca63','#fad860','#f3a43b','#fad860','#f3a43b','#60c0dd','#c6e579','#f4e001','#f0805a','#26c0c0','#9bca63','#fad860','#f3a43b','#fad860','#f3a43b','#60c0dd','#c6e579'],

          }
        ]
      },
    }
  },
  mounted() {
    this.processData();
    this.initChart();
  },
  methods:{
    initChart: function () {
      this.chartOptions.series[0].data = this.chart_data;
      this.chartOptions.series[0].color = this.color_list;
      // console.log(this.chartOptions);
      this.myChart = echarts.init(this.$refs["chart"]);
      this.chartOptions && this.myChart.setOption(this.chartOptions);
    },
    processData: function (){
      this.unprocess_data.sort((a,b)=> b.value-a.value);
      this.chart_data = this.unprocess_data.slice(0,this.top_num);
      let other_death = 0;
      for (let i=this.top_num; i<this.unprocess_data.length; i++){
        if (this.unprocess_data[i].name==="HIV/AIDS"){
          this.chart_data.push(this.unprocess_data[i]);
        }else{
          other_death += this.unprocess_data[i].value;
        }
      }
      this.chart_data.push({value:other_death, name:"Other Death Causes"});
      this.chart_data.forEach(item=>{
        // Get color code according to the death cause name
        this.color_list.push(colorcode.filter(color_death=>color_death.name===item.name)[0].value);
        if (item.name==="HIV/AIDS"){
          item.selected=true;
          item.label = {
            show: true,
            position:'inner',
            fontWeight: 'bold',
            formatter: '{b}',

          };
          item.labelLine = {
            show: true,
            showAbove: true,
            length: 30,
            width: 2,
          };
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
