<template>
<!-- PART03: Sustainable Development Goals -->
  <div>
    <SessionBanner 
      img-url="https://www.unicef.de/image/119276/21x9/974/417/fbb2e2b79663de224ed9aa93d45344aa/OC/hiv-aids-logenzo-malawiuni201842.jpg"
      title="Sustainable Development Goals"
      subtitle="Goal 3: Ensure healthy lives and promote well-being for all at all ages"/>
    <div class="tm-row tm-about-row" style="background-color:#279B48;">
      <div class="tm-section-1-r" style="width:20%; padding:0px">
        <img src="../../public/images/SDG.png" style="width:100%; padding"/>
      </div>
      <div class="tm-section-1-l" style="width:70%; padding-top:1%; padding-left:3%">
        <h6 class="text-white"><span style="font-size: 150%">Goal 3.3: By 2030, end the epidemics of AIDS</span>, tuberculosis, malaria and neglected tropical diseases and combat hepatitis, water-borne diseases and other communicable diseases.</h6>
      </div>
    </div>

    <div class="tm-row tm-about-row">
      <div class="tm-section-1-l" style="width:40%; padding-top:5%; padding-left:2%">
        <span style="font-size:150%"><strong>UNAIDS</strong></span> is leading the global effort to end AIDS as a public health threat by 2030 as part of the Sustainable Development Goals.<br><br>
        The estimated 1.7 million people who acquired HIV worldwide in 2019 marked a 23% decline in new HIV infections since 2010. This was the lowest annual number of new infections since 1989. Meanwhile, increased access to antiretroviral therapy has averted an estimated 12.1 million AIDS-related deaths since 2010.
      </div>
      <div class="tm-section-1-r, q-pa-md" style="width:60%;">
        <UNProgress />
      </div>
    </div>
  </div>
</template>

<script>

import SessionBanner from "components/tools/SessionBanner";
import UNProgress from 'components/SDG/UNProgress.vue';

export default {
  name: '   SDG',
  components: {
    SessionBanner,
    UNProgress
  },
  data() {
    return {

    };
  },
  computed: {

  },
  mounted() {

  },

  methods: {

  },

  watch:{

  }
};
</script>
<style lang="sass" scoped>

</style>
