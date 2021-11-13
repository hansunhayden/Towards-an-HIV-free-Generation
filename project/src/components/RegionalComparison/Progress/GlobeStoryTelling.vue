<template>
<!--  Two tabs to compare Sub-Saharan Africa and Western Europe -->
  <div class="q-pa-md">
    <div class="q-gutter-y-md" style="width: 90vw">
        <q-tabs
          v-model="tab"
          dense
          active-color="negative"
          indicator-color="negative"
          align="center"
          narrow-indicator
        >
          <q-tab name="ssa" label="Sub-Saharan Africa"/>
          <q-separator vertical />
          <q-tab name="eu" label="Western Europe" />
        </q-tabs>
        <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="ssa">
<!--            Sub-Saharan Africa Map and Charts -->
            <RegionSSA/>
          </q-tab-panel>

          <q-tab-panel name="eu">
<!--            Western Europe Map and Charts -->
            <RegionWEU/>
          </q-tab-panel>

        </q-tab-panels>
        <q-tabs
          v-model="tab"
          dense
          active-color="secondary"
          indicator-color="secondary"
          align="center"
          narrow-indicator
          switch-indicator
          content-class="text-h4"
        >
          <q-tab name="ssa" label="Sub-Saharan Africa"/>
          <q-separator vertical />
          <q-tab name="eu" label="Western Europe" />
        </q-tabs>
    </div>
  </div>

</template>

<script>

import RegionSSA from "components/RegionalComparison/Progress/RegionSSA";
import RegionWEU from "components/RegionalComparison/Progress/RegionWEU";
export default {
  name: 'GlobeStoryTelling',
  components: {RegionWEU, RegionSSA, },
  data() {
    return {
      tab: "ssa",
    };
  },
  computed: {
  },
  mounted() {
  },

  methods: {

  },

  watch: {
  },

};
</script>
<style lang="scss" scoped>
.grid-layout {
  height: 100%;
  width: 100%;
}
.stepper-container {
  height: 100%;
  width: 100%
}
</style>
