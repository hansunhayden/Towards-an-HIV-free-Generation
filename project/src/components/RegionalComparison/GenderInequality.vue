<template>
<div class="center">
  <subsession-title title="Inequality between genders"/>
  <div class="q-ma-md">
    <q-space class="q-ma-lg"/>
    <div style="padding:1%">
      <strong>
        HIV risk among adults is higher among specific ages, genders and subpopulations by region, depending on the type of epidemic within the countries, cities and communities of the region.
      </strong>
    </div>
    <div style="padding:1%">
      <strong class="text-secondary">In Sub-Saharan Africa, adolescent girls and young women (aged 15 to 24 years) in particular are at higher risk of HIV infection</strong>: they accounted for about one in four new infections, despite comprising only 10% of the population. In the region most affected by HIV, eastern and southern Africa, adolescent girls and young women accounted for 30% of new infections.  <strong class="text-secondary">Outside of Sub-Saharan Africa, men accounted for the majority of new adult HIV infections.</strong>
    </div>
    <q-space class="q-ma-lg"/>
    <div class="center-div" style="width: 80%;">
      <women-share-picutre-bar/>
    </div>
    <div class="row items-stretch q-mt-sm q-mb-lg">
      <div class="col-12 col-md-6 q-pt-lg" ref="mapviewContainer">
        <div style="padding-left:2%" class="q-mb-lg">
          The trend in AIDS-related deaths in both Sub-Saharan Africa and Western Europe shows the opposite: <strong><span class="text-secondary">more men tend to to die from AIDS every year than women</span></strong>. The reasons for differences in prevalence and death rates are complex; however, in general, <strong>across Sub-Saharan Africa women tend to be infected with HIV earlier than men and survive longer</strong> (explaining both the higher prevalence and lower annual AIDS deaths in women). There are a number of gender inequality and social norm issues which result in higher prevalence of HIV in females across many countries; women are at greater risk when they have a limited role in sexual decision-making and protection, role rates of sexual education and higher rates of transactional sex. After testing positively, women tend to actively receive the treatments - the coverage of HIV treatment among women is higher than that among men as we mentioned before.
        </div>
        <div style="padding-left:2%">
          In children with HIV, transmission has typically occurred from the mother (mother-to-child-transmission; MTCT) either during pregnancy or childbirth, or through breastfeeding. <strong class="text-secondary">Across Sub-Saharan Africa, many countries with high share of women living with HIV also reflect larger number of children with HIV/AIDS.</strong>
          <!-- The map of Children with HIV shows the total number of children aged 14 years old and under who are living with HIV per country since 1990. -->
        </div>
      </div>
      <div class="col-12 col-md-6 q-pa-lg" ref="mapviewContainer">
        <q-img src="images/ART.jpg"/>
      </div>
    </div>
    <div class="center-div" style="width: 90vw">
      <WomenShareMap/>
      <!--<q-tabs
        v-model="tab"
        dense
        class="q-ma-xs"
        active-color="secondary"
        indicator-color="secondary"
        align="center"
        narrow-indicator
      >
        <q-tab name="women" label="Women Living with HIV" />
        <q-separator vertical />
        <q-tab name="child" label="Children with HIV" />
      </q-tabs>
      <q-tab-panels v-model="tab" animated class="q-ma-xs">
        <q-tab-panel name="women">
          <div class="center-div">

          </div>
        </q-tab-panel>
        <q-tab-panel name="child">
          <div class="center-div">
            <ChildrenHIVMap/>
          </div>
        </q-tab-panel>
      </q-tab-panels>
      <q-tabs
        v-model="tab"
        dense
        class="q-ma-xs"
        active-color="secondary"
        indicator-color="secondary"
        align="center"
        narrow-indicator
        switch-indicator
      >
        <q-tab name="women" label="Women Living with HIV" />
        <q-separator vertical />
        <q-tab name="child" label="Children with HIV" />
      </q-tabs>
      -->
    </div>
    <q-space class="q-ma-xl"/>
  </div>

</div>
</template>

<script>
import WomenShareMap from "components/RegionalComparison/GenderInequality/WomenDistriution/WomenShareMap";
import WomenSharePicutreBar from "components/RegionalComparison/GenderInequality/WomenDistriution/WomenSharePicutreBar";
//import ChildrenHIVMap from "components/RegionalComparison/GenderInequality/ChildrenDistribution/ChildrenHIVMap";

import SubsessionTitle from "components/tools/SubsessionTitle";

export default {
  name: "WomenShare",
  components: {WomenSharePicutreBar, SubsessionTitle, WomenShareMap}, //ChildrenHIVMap,
  data() {
    return {
      tab: "women"
    }
  },
}
</script>

<style lang="scss" scoped>
.center-div {
  margin: auto;
  //border: 1px solid;
  padding: 1px;
}
</style>
