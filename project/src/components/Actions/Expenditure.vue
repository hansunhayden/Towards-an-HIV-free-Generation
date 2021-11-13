<template>
<div>
  <div class="q-ml-lg q-mr-lg grid-layout">
    <div class="row items-stretch">
      <div class="col-12 col-md-6 q-pt-lg">
        <div class="q-mt-xl">
          <div class="q-mb-md" style="line-height: 1.5">
            In 2019, <strong class="text-secondary">around $330 million</strong> were invested in the operation in strategy result areas by UNAIDS, which takes around three quarters of its total funding resource.
          </div>
          <div class="q-mb-md" style="line-height: 1.5">
            The resource for prevention and treatment of HIV in <strong>low-to-middle income countries</strong> of the world in 2016 is <strong>around $19.2 billion</strong>. However, according to the estimation of UNAIDS, the type of funding required to achieve 2030 targets should be <strong>more than $25 billion per year</strong>.
          </div>
          <div class="q-mb-md" style="line-height: 1.5">
            <strong>
              Thus, governments may allocate more resource in HIV-related measurements to follow up the 2030 goal.
            </strong>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-6 q-pa-lg">
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
            <q-tab name="current" label="Funding Resource" />
            <q-tab name="expect" label="Estimate Requirement" />
          </q-tabs>
          <q-separator />
          <q-tab-panels v-model="tab" animated>
            <q-tab-panel name="current">
              <expenditure-sunburst/>
            </q-tab-panel>
            <q-tab-panel name="expect">
              <expenditure-estimation-line/>
            </q-tab-panel>
          </q-tab-panels>
        </q-card>
      </div>
    </div>
  </div>
</div>
</template>

<script>


import ExpenditureSunburst from "components/Actions/ActionsCharts/ExpenditureSunburst";
import ExpenditureEstimationLine from "components/Actions/ActionsCharts/ExpenditureEstimationLine";
export default {
  name: "Expenditure",
  components: {ExpenditureEstimationLine, ExpenditureSunburst},
  data() {
    return{
      tab:'current'
    }
  }
}
</script>

<style scoped>

</style>
