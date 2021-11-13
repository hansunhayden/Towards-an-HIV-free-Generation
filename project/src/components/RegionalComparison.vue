<template>
<!-- PART04: Heterogeneous Distribution -->
  <div>
    <q-page>
      <SessionBanner img-url="images/religion.jpg"
                     title="Heterogeneous Distribution"
                     subtitle="The spreading of HIV/AIDS is not evenly distributed. Some regions require special attention in meeting SDG."
      />
      <DeathByCause/>
    </q-page>
    <q-space/>
    <q-page>
      <Progress/>
    </q-page>
    <q-space/>
    <q-page>
      <GenderInequality/>
    </q-page>

  </div>
</template>

<script>
import SessionBanner from "components/tools/SessionBanner";

import DeathByCause from "components/RegionalComparison/DeathByCause";
import Progress from "components/RegionalComparison/Progress";
import GenderInequality from "components/RegionalComparison/GenderInequality";

export default {
  name: 'RegionalComparison',
  components: {
    SessionBanner,
    DeathByCause, Progress, GenderInequality},
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
