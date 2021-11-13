<template>
  <div class="q-ml-md q-mr-md grid-layout">
    <div class="row items-stretch q-mt-sm q-mb-lg">
      <div class="col-12 col-md-6 q-pa-lg" ref="mapviewContainer">
        <div class="height:500px; width:100%">
          <q-resize-observer @resize="onResize" />
<!--          Map -->
          <GeomapEcharts :region="regionName"
                         :geo-json="geoJson"
                         :death-rate-json="deathRateJson"
                         :death-share-json="deathShareJson"
                         @dataChange="updateTimeseriesData"
                         @titleChange="updateTimeseriesTitle"
                         @isActive="updateMapActive"
                         ref="ssaMap"
          />
        </div>
      </div>
      <div class="col-12 col-md-6 items-stretch">
        <div style="height:500px; width:100%" class="column">
          <div class="col-10" >
<!--            Line Chart -->
            <TimeseriesLineChart :timeseries-data="timeseriesData"
                                 :timeseries-chartinfo="timeseriesChartLegend"
                                 :baseline-data="baselineData"
                                 :baseline-legend="regionName"
                                 :title="timeseriesChartTitle"
            />
          </div>
          <div class="col-2 self-center text-center text-center" >
            <div class="self-center q-pa-lg text-center bg-grey-2 round-borders-lg" style="border-radius:15px;">
              <q-btn
                outline
                rounded
                @click="changeMapData"
              >{{mapActive ? 'Show Death Rates':'Show New Infections of HIV/AIDS' }}</q-btn>
            </div>
          </div>
        </div>
      </div>
    </div>
    <q-space class="q-mt-lg q-mb-lg"/>
<!--    Number counter -->
    <div  v-intersection="onIntersection" class="q-mt-lg self-center q-mr-xl">
      <div class="row justify-evenly text-center">
        <div class="col-12 col-md-4 ">
          <NumberCounter number="30" unit="percent" title="declined in death rate since 2000" ref="counter1"/>
        </div>
        <div class="col-12 col-md-4 ">
          <NumberCounter number="38" unit="percent" title="declined in new infections since 2000" ref="counter2"/>
        </div>
        <div class="col-12 col-md-4 ">
          <NumberCounter number="26" unit="percent" title="of infections are among adolescent girls and young women in 2019" ref="counter3"/>
        </div>
      </div>
    </div>
    <q-space/>

    <div>
      Although Sub-Saharan Africa shows the highest death rates over the world, the region made a progress in controlling the epidemics of the disease since 21st century.  The decrease in new HIV infections in Sub-Saharan Africa since 2010 is larger than in any other region.

      According to UNAIDS, the new HIV infections have declined by 38% and AIDS-related death by 30% in the region since 2010. Adolescent girls and young women account for 26% of new infections in the region, which is the key population of new HIV infections in Sub-Saharan Africa. This proportion also drops 37% since 2010.
    </div>
  </div>
</template>

<script>
import NumberCounter from "components/tools/NumberCounter";

import TimeseriesLineChart from "components/RegionalComparison/Progress/TimeseriesLineChart";
import GeomapEcharts from "components/RegionalComparison/Progress/GeomapEcharts";

import {deathRateAllSSA, infectionRateAllSSA} from "assets/json/geomapData";
import {ssajson, deathRateSSA, infectionRateSSA} from "assets/json/geomapData";


export default {
  name: "RegionSSA",
  components: {NumberCounter, GeomapEcharts, TimeseriesLineChart, },
  data() {
    return {
      regionName: "Sub-Saharan Africa",
      timeseriesData: [],
      timeseriesChartLegend: "",
      timeseriesChartTitle: "HIV Death Rates",
      baselineData: deathRateAllSSA,

      deathRateSeriesName:'HIV Death Rates',
      deathShareSeriesName:'New Infections of HIV/AIDS',

      mapActive: false,
      geoJson: ssajson,
      deathRateJson: deathRateSSA,
      deathShareJson: infectionRateSSA,
    };
  },
  methods: {
    onResize (size) {
    },

    updateTimeseriesData(timeseriesList, title, country){
      // Update line chart data
      this.timeseriesData = timeseriesList;
      this.timeseriesChartLegend = country;
      this.timeseriesChartTitle = title;
    },
    updateTimeseriesTitle(title){
      // Update line chart title
      this.timeseriesChartTitle = title;
    },
    animate(){
      // Trigger animation of number counter
      this.$refs.counter1.startAnim();
      this.$refs.counter2.startAnim();
      this.$refs.counter3.startAnim();
    },
    onIntersection(){
      this.animate()
    },
    updateMapActive(val){
      this.mapActive = val;
    },
    changeMapData(){
      // Update map data
      this.$refs.ssaMap.toggle();
    }
  },

  watch: {
    timeseriesChartTitle: function(val){
      console.log("update title "+val);
      if(val===this.deathRateSeriesName){
        this.baselineData = deathRateAllSSA;
      }else if(val===this.deathShareSeriesName){
        this.baselineData = infectionRateAllSSA;
      }
    },
  },
}
</script>

<style  lang="sass" scoped>
.row > div
  padding: 10px 15px
                  //background: rgba(86,61,124,.15)
  //border: 1px solid rgba(86,61,124,.2)
.row + .row
  margin-top: 1rem
</style>
