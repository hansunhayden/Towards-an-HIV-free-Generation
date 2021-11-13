<template>
<!--  Analyzing death by causes -->
  <div>
    <subsession-title title="In Sub-Saharan Africa, HIV/AIDS is the leading cause of deaths"/>
    <div class="q-pa-lg">
      <div class="row">
<!--        Text -->
        <div class="col-12 col-md">
          <div class="q-pr-md q-pt-md">
            <q-space class="q-ma-lg"/>
            <div class="q-mb-md">
              <article style="line-height:1.5">
                HIV one of the largest killers globally. <span style="font-size:120%;"><strong>1.8%</strong></span> of deaths were caused by HIV/AIDS in 2017.
              </article>
            </div>
            <div class="q-mb-md">
              <article>
                This share is high, but masks the wide variations in the toll of HIV/AIDS across the world. In <strong><span class="text-secondary">Western Europe</span></strong>, HIV/AIDS caused <span style="font-size:120%"><strong>less than 0.1%</strong></span> of deaths. In some countries, this share was much higher – across <strong><span class="text-secondary">Sub-Saharan Africa</span></strong>, it’s <span style="font-size:120%"><strong>the leading cause of death</strong></span>.
              </article>
            </div>
            <div class="q-mb-md">
              <article style="line-height:1.5">
                For countries in southern Sub-Saharan Africa, deaths from HIV/AIDS are more than <span style="font-size:120%"><strong>50%</strong></span> higher than deaths from heart disease, and more than twice that of cancer deaths. If we look at the breakdown for <span style="font-size:120%"><strong>South Africa, Botswana or Mozambique</strong></span> – we see that HIV/AIDS tops the list.
              </article>
            </div>
          </div>
        </div>
<!--        Line charts for three countries -->
        <div class="col-12 col-md items-end q-pa-md">
          <div class="q-gutter-y-md q-ma-sm" style="max-width: 95%">
            <q-card flat bordered>
              <q-tabs
                v-model="tab"
                dense
                class="text-grey"
                active-color="primary"
                indicator-color="primary"
                align="justify"
                narrow-indicator
              >
                <q-tab name="sa" :label="sa_name" />
                <q-tab name="moz" :label="moz_name" />
                <q-tab name="bot" :label="bot_name" />
              </q-tabs>
              <q-separator />
              <q-tab-panels v-model="tab" animated>
                <q-tab-panel name="sa">
                  <DeathByCauseBarChart :series-data="sa_series" :name="sa_name" :categories="sa_categories"/>
                </q-tab-panel>
                <q-tab-panel name="moz">
                  <DeathByCauseBarChart :series-data="moz_series" :name="moz_name" :categories="moz_categories"/>
                </q-tab-panel>
                <q-tab-panel name="bot">
                  <DeathByCauseBarChart :series-data="bot_series" :name="bot_name" :categories="bot_categories"/>
                </q-tab-panel>
              </q-tab-panels>
            </q-card>
          </div>
        </div>
      </div>
    </div>
<!--    Pie charts for three regions -->
    <div class="q-mt-sm q-mb-lg">
      <div class="text-weight-bold text-center text-h6">Percentage of deaths by cause, 2017</div>
      <div class="q-ma-sm items-center">
        <div class="row">
          <div class="col-12 col-md">
            <DeathByCausePieChart :data="ssa_percent_data" :name="ssa_name"/>
          </div>
          <div class="col-12 col-md">
            <DeathByCausePieChart :data="world_percent_data" :name="world_name"/>
          </div>
          <div class="col-12 col-md">
            <DeathByCausePieChart :data="ch_percent_data" :name="ch_name"/>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import {ssa_deathCause, ssa_deathNumByCause, ssa_percent,
  ch_deathNumByCause,
  weu_percent,
  world_deathCause, world_deathNumByCause, world_percent,
  south_africa_deathNumByCause, south_africa_deathCause,
  mozambique_deathCause, mozambique_deathNumByCause,
  botswana_deathCause, botswana_deathNumByCause,
} from "assets/json/deathByCause";
import DeathByCauseBarChart from "components/RegionalComparison/DeathByCause/DeathByCauseBarChart";
import DeathByCausePieChart from "components/RegionalComparison/DeathByCause/DeathByCausePieChart";
import SubsessionTitle from "components/tools/SubsessionTitle";

export default {
  name: "DeathByCauseComparison",
  components: {SubsessionTitle, DeathByCausePieChart, DeathByCauseBarChart},
  data(){
    return{
      tab: 'sa',
      ssa_series: ssa_deathNumByCause,
      ssa_name: "Sub-Saharan Africa",
      ssa_categories: ssa_deathCause,
      ssa_percent_data: ssa_percent,
      sa_series: south_africa_deathNumByCause,
      sa_name:"South Africa",
      sa_categories: south_africa_deathCause,
      moz_series: mozambique_deathNumByCause,
      moz_name:"Mozambique",
      moz_categories: mozambique_deathCause,
      bot_series: botswana_deathNumByCause,
      bot_name:"Botswana",
      bot_categories: botswana_deathCause,
      ch_series: ch_deathNumByCause,
      ch_name: "Western Europe",
      ch_percent_data: weu_percent,
      world_series: world_deathNumByCause,
      world_name: "World",
      world_categories: world_deathCause,
      world_percent_data: world_percent,
    }
  }
}
</script>

<style scoped>
#splitter-container{
  max-height: 800px;
}

.highlight{
  background-color: #11524b; border-radius: 5px; padding: 5px; margin: 2px; font-size:120%; color: white;
}
</style>
