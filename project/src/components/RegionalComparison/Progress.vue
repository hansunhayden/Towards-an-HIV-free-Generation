<template>
<!--  Progress in Sub-Saharan Africa and Western Europe-->
  <div>
    <subsession-title title="Progress in Sub-Saharan Africa and Western Europe"/>
    <div class="center  q-pa-md">
      <q-space class="q-ma-lg"/>
      <div style="padding:1%;">
        <strong>Different regions face different challenges in fighting with HIV/AIDS. We use <span class="text-secondary">Sub-Saharan Africa</span> and <span class="text-secondary">Western Europe</span> as our case studies.</strong>
      </div>
      <div style="padding:1%;">
        The large health burden of HIV/AIDS across Sub-Saharan Africa is also reflected in death rates. Death rates measure the number of deaths from HIV/AIDS per 100,000 individuals in a country or region. Across the world, most countries have a rate of less than 10 deaths per 100,000. Across Europe the death rate is less than 1 per 100,000. <strong class="text-secondary">Across Sub-Saharan Africa the death rates are much higher than the other regions.</strong> Most countries in the South of the region had rates greater than 100 per 100,000. South Africa, Mozambique, Lesotho and Eswatini are the countries with the highest death rate across the region.
      </div>
      <div style="padding:1%;">
        Since the first clinically observation of HIV/AIDS in 1981 in the United States, HIV/AIDS has spread over the world and is marked as one of the most fatal disease. The 1990s saw a substantial increase in the number of people infected with HIV and dying of AIDS. The peak of death rates was seen in 2005 and peak of new infections was seen in 2000 across Sub-Saharan Africa. Across Western Europe,  the death rates of HIV/AIDS increased rapidly in the early 1990s, but decreased quickly to less than 2 per 100,000 then. Since 2010, the number is steadily decreasing to less than 1 per 100,000 people.  Although we can see the steady decrease of infection rates in Western Europe, the infection rates in some countries like Belgium and Austria increased from 0.05 to 0.2 since 1990.
      </div>
    </div>
    <div class="center flex flex-center">
      <GlobeStoryTelling/>
    </div>
    <q-space class="q-ma-xl"/>
  </div>
</template>

<script>
import GlobeStoryTelling from "components/RegionalComparison/Progress/GlobeStoryTelling";
import SubsessionTitle from "components/tools/SubsessionTitle";

export default {
  name: "DeathRate",
  components: {SubsessionTitle, GlobeStoryTelling,}
}
</script>

<style scoped>

</style>
