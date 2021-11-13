<template>
<!--  Layout for showing 3D Globe map -->
  <div class="tm-row tm-about-row">
      <div class="tm-section-1-l  q-pa-md grid-layout" ref="mapviewContainer" style="width:50%">
        <div>
            <q-resize-observer @resize="onResize" />
            <SSAViewer ref="mapViewer"
                      class="flex flex-center"
                      :width="globeWidth" :height="globeHeight"/>
        </div>
      </div>
      <div class="tm-section-1-r" style="width:50%">

      <q-stepper
        v-model="step"
        vertical
        color="primary"
        animated
      >
        <div style="height: 10%" class="q-ma-md">
          <q-btn v-bind:class="[step === 1 ? 'active-button' : '']" style="margin-left:1%; margin-right:1%;" rounded label="Infection Rate" @click="$refs.mapViewer.showInfectionRate(); step = 1"/>
          <q-btn v-bind:class="[step === 2 ? 'active-button' : '']" style="margin-right:1%;" rounded label="Death Rate" @click="$refs.mapViewer.showDeathRate(); step = 2"/>
          <!-- <q-btn  style="margin-right:1%;" push color="primary" label="Share of Death" @click="$refs.mapViewer.showShareDeath(); step = 2"/> -->
        </div>
        <q-step
          :name="1"
          title="HIV Infections"
          icon="bookmark"
          active-icon="bookmark"
          :done="step > 1"
        >
        In 2019, there were <strong><span style="font-size:150%">38.0</span></strong> million people living with HIV,
        <strong><span style="font-size:150%">36.2</span></strong> million adults and
        <strong><span style="font-size:150%">1.8</span></strong> million children (0–14 years).
        <br>
        <strong><span style="font-size:150%">75.7</span></strong> million people have become infected with HIV since the start of the epidemic (end 2019).<br>
        <strong><span style="font-size:150%">1.7</span></strong> million people became newly infected with HIV in 2019.
        <br/>
          <div class="row q-pl-sm q-mt-md justify-center">
            <div>
              <a class="text-body2">The share of people aged 15 to 49 years old who are infected with HIV.</a> <br />
              <span id="bar"></span>
              <br />
              <span class="start-text text-body2">0.0</span>
              <span class="end-text text-body2">28%</span>
            </div>
          </div>
          <q-stepper-navigation>
            <q-btn rounded icon="keyboard_arrow_down" @click="onStepChange(2)" />
          </q-stepper-navigation>
        </q-step>
        <q-step
          :name="2"
          title="HIV Related Deaths"
          icon="bookmark"
          active-icon="bookmark"
        >
          <strong><span style="font-size:150%">690,000</span></strong> people died from AIDS-related illnesses in 2019.
          <br>
          <strong><span style="font-size:150%">32.7</span></strong> million people have died from AIDS-related illnesses since the start of the epidemic (end 2019).
          <br/>
          <div class="row q-pl-sm q-mt-md justify-center">
            <div>
              <a class="text-body2">The number of deaths from HIV/AIDS per 100,000 people.</a> <br />
              <span id="negative-bar"></span>
              <br />
              <span class="start-text text-body2">0.0</span>
              <span class="end-text text-body2">250</span>
            </div>
          </div>
          <q-stepper-navigation>
            <q-btn rounded icon="keyboard_arrow_up" @click="onStepChange(1)" class="q-ml-sm" />
          </q-stepper-navigation>
        </q-step>
      </q-stepper>
    </div>
  </div>
</template>

<script>
import SSAViewer from "components/CurrentSituation/GlobeGLComponent/SSAViewer";

export default {
  name: "GlobeViewLayout",
  components: {SSAViewer},
  data() {
    return {
      globeSizePercent: 0.99, //use 99% of the div
      globeWidth: 0,
      globeHeight:0,
      step: 1
    };
  },
  mounted() {
    this.globeWidth = this.$refs.mapviewContainer.getBoundingClientRect().width * this.globeSizePercent;
    this.globeHeight = this.$refs.mapviewContainer.getBoundingClientRect().height * this.globeSizePercent;
  },
  methods: {
    onResize(size) {
      // Adjust the globe size when the window resized
      this.globeWidth = size.width * this.globeSizePercent;
      this.globeHeight = size.height * this.globeSizePercent;
      this.$refs.mapViewer.resizeMap(this.globeWidth, this.globeHeight);
    },
    onStepChange(step_idx){
      this.step = step_idx;
      if(step_idx===1){
        this.$refs.mapViewer.showInfectionRate();
      }else if(step_idx===2){
        this.$refs.mapViewer.showDeathRate();
      }
    },
  },
  watch: {
  }
}
</script>

<style scoped>
.active-button {
  background-color: rgba(39, 155, 72, 0.2);
}
#bar {
  display: inline-block;
  width: 95%;
  height: 15px;
  margin-right: 0;
  margin-left: 10px;
  background: linear-gradient(
    to right,
    rgb(255, 255, 255),
    rgb(224, 1, 1),
    rgb(120, 0, 0)
  );
}
#negative-bar {
  display: inline-block;
  width: 95%;
  height: 15px;
  margin-right: 0;
  margin-left: 10px;
  background: linear-gradient(
    to right,
    rgb(3, 218, 253),
    rgb(250, 250, 250),
    rgb(250, 230, 0)
  );
}

.start-text {
  display: inline-block;
  width: 50%;
  height: 15px;
  margin-right: 0px;
  margin-left: 0;
  text-align: left;
}


.end-text {
  display: inline-block;
  width: 50%;
  height: 15px;
  margin-right: 0px;
  margin-left: 0;
  padding-right: 0px;
  text-align: right;
}
</style>
