<template>
  <div class="q-ml-md q-mr-md grid-layout">
    <div class="row items-stretch">
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
                         ref="weuMap"
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
          <NumberCounter number="81" unit="percent" title="of people living with HIV were on treatment in 2019." ref="counter1"/>
        </div>
        <div class="col-12 col-md-4 ">
          <NumberCounter number="96" unit="percent" title="of HIV infections were among key populations and their sex partners in 2019." ref="counter3"/>
        </div>
        <div class="col-12 col-md-4 ">
          <NumberCounter number="36" unit="percent" title="of total infections were among young gay men and other men who have sex with men (aged 15 to 24 years) in 2019." ref="counter2"/>
        </div>
      </div>
    </div>
    <div>
      Strong HIV responses in Western Europe have seen this high-income region achieve an incidence: steady reductions in new HIV infections and that most people living with HIV are accessing treatment and living long and healthy lives.
      HIV testing and treatment coverage in the region is approaching the 2020 targets, with 88% of people living with HIV knowing their HIV status and 81% on treatment.
    </div>
    <div>
      <br>
      High prevalence remains high among key populations and their sex partners, with 96% HIV infections in 2019. Gay men and other men who have sex with men accounted for nearly two thirds of new HIV infections in the region in 2019. More than one third (36%) of total infections were among young gay men and other men who have sex with men (aged 15 to 24 years).
    </div>
    <div>
      <br>
      This aggregate success obscures many challenges. Across the region, undocumented migrants living in insecure and precarious situations have less access to HIV services, including HIV treatment and new prevention tools.
    </div>
  </div>
</template>

<script>
import TimeseriesLineChart from "components/RegionalComparison/Progress/TimeseriesLineChart";
import GeomapEcharts from "components/RegionalComparison/Progress/GeomapEcharts";

import {deathRateAllEU, infectionRateAllEU} from "assets/json/geomapData";
import {weujson, deathRateEU, infectionRateEU} from "assets/json/geomapData";

import NumberCounter from "components/tools/NumberCounter";

export default {
  name: "RegionWEU",
  components: {NumberCounter, GeomapEcharts, TimeseriesLineChart, },
  data() {
    return {
      regionName: "Western Europe",
      timeseriesData: [],
      timeseriesChartLegend: "",
      timeseriesChartTitle: "HIV Death Rates",
      baselineData: deathRateAllEU,

      deathRateSeriesName:'HIV Death Rates',
      deathShareSeriesName:'New Infections of HIV/AIDS',

      mapActive: false,
      geoJson: weujson,
      deathRateJson: deathRateEU,
      deathShareJson: infectionRateEU,
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
      this.$refs.weuMap.toggle();
    }
  },

  watch: {
    timeseriesChartTitle: function(val){
      if(val===this.deathRateSeriesName){
        this.baselineData = deathRateAllEU;
      }else if(val===this.deathShareSeriesName){
        this.baselineData = infectionRateAllEU;
      }
    },
  },
}
</script>

<style lang="sass" scoped>
.row > div
  padding: 10px 15px
//background: rgba(86,61,124,.15)
//border: 1px solid rgba(86,61,124,.2)
.row + .row
  margin-top: 1rem
</style>

