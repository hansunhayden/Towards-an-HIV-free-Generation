<template>
    <SubsessionTitle title="Antiretroviral Therapy Treatment" />
    <div v-intersection.once="onIntersection" class="q-pa-md" style="margin-top:0px; padding-top:0px">
      <transition class="fade-in-text" style="font-size:140%">
        <div v-if="show" style="text-align:left; color:#5A5A5A">
          <br>
          Although there is no cure for HIV, extremely effective treatment called antiretroviral therapy (ART) is available which can keep the virus under control.<br>
          Someonewith HIV who is diagnosed early and responds well to treatment can lead an active, normal life and have a near normal life expectancy.<br>
          <span style="font-size:120%"><strong>25.4</strong></span> million people were accessing antiretroviral therapy in 2019.
        </div>
      </transition>
    </div>
    <div>
      <h6>

      </h6>
    </div>
    <q-page>
      <section class="tm-mb-0 content-body">
          <div class="tm-row tm-about-row">
              <div class="tm-section-1-l center-div" style="margin:1%; width:50%;">
                  <WorldARTTrend/>
              </div>
              <div class="tm-section-1-r center-div" style="width:50%; height:400px; margin:1%">
                 <q-stepper
                  v-model="step"
                  ref="stepper"
                  animated
                  done-color="#279B48"
                  active-color="#279B48"
                  inactive-color="#b8bcc0"
                  class="no-shadow"
                >

                  <q-step
                    :name="1"
                    title="Extend Life Span"
                    icon="add_comment"
                    :done="step > 1"
                  >
                    <h2>People who use ART are living longer</h2>
                    ART not only saves lives but also gives a chance for people living with HIV/AIDS to live long lives. Without ART very few infected people survive beyond ten years.<br>
                    Today, a  person living in a high-income country who started ART in their twenties can expect to live for another 46 years — that is well into their 60s.<br>
                    While the life expectancy of people living with HIV/AIDS in high-income countries has still not reached the life expectancy of the general population, we are getting closer to this goal.
                  </q-step>

                  <q-step
                    :name="2"
                    title="Prevent New Infections"
                    icon="add_comment"
                  >
                    <h2>ART prevents new HIV infections</h2>
                    ART reduces the number of viral particles present in an HIV-positive individual and therefore, the likelihood of passing the virus to another person decreases.<br>
                    The chances of HIV positive mother transmitting the virus to a child are between 15% and 45%. Effective prevention of mother-to-child transmission (PMTCT) services can reduce the chances of virus transmission to newborn to 5%. From the chart (link to among young children), we could tell an remarkable decrease in children infection, as a result of antiretroviral therapy across the world.
                  </q-step>

                  <template v-slot:navigation>
                    <q-stepper-navigation>
                      <q-btn v-if="step===1" flat @click="$refs.stepper.next()" label="Continue"/>
                      <q-btn v-if="step > 1" flat @click="$refs.stepper.previous()" label="Back" class="q-ml-sm" />
                    </q-stepper-navigation>
                  </template>
                </q-stepper>
              </div>
          </div>
      </section>
    </q-page>
    <WorldARTRate />
</template>

<script>
import WorldARTRate from "components/Actions/ActionsCharts/WorldARTRate"
import WorldARTTrend from "components/Actions/ActionsCharts/WorldARTTrend"
import SubsessionTitle from "components/tools/SubsessionTitle"

export default {
  name: "ART",
  components: {
    WorldARTRate,
    WorldARTTrend,
    SubsessionTitle
  },
  data() {
    return {
      step: 1,
      show: false
    }
  },
  methods: {
    onIntersection(entry) {
      // When the view intersects with the div, trigger animation to show the div content
      this.show = entry.isIntersecting
    },
  },
}
</script>

<style  lang="scss" scoped>
.center-div {
  margin: auto;
  padding: 1px;
}
</style>
