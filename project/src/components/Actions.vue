<template>
<!-- PART06: Actions: treatment & prevention, expenditure -->
  <div>
    <q-page>
      <session-banner img-url="images/treatment_1_1440.jpg"
                      title="Take Actions"
                      subtitle="Increased access to antiretroviral therapy has averted an estimated 12.1 million AIDS-related deaths since 2010."/>
      <SubsessionTitle title="Prevention and Treatment" />
      <div class="q-pa-lg">
        <div v-intersection.once="onIntersection" class="q-pa-md" style="margin-top:0px; padding-top:0px">
          <transition class="fade-in-text">
            <div v-if="show" style="text-align: center; font-size: 150%; color:#5A5A5A">
              12.1 million AIDS-related deaths were saved because of the increased access to antiretroviral therapy since 2010.
            </div>
          </transition>
        </div>
        <div>
          Some epidemic models have suggested that universal HIV testing and treatment, combined with primary prevention, could reduce HIV transmission to such low levels that <strong>the epidemic could eventually be eliminated</strong>.<br>
          Currently, the treatments are mainly in two categories: <strong>Antiretroviral Therapy (ART) and by prevention</strong>.
        </div>

        <div class="tm-row tm-social-row" style="margin-bottom:0px;" id="ways">

          <!-- content for ART -->
          <div class="tm-icon">
            <div class="tm-icon-inner">
              <q-card class="my-card">
                <q-video src="https://www.youtube.com/embed/0TipTogQT3E" />

                <q-card-section>
                  <div class="text-h4">ART</div>
                  <div class="text-subtitle2">Antiretroviral Therapy</div>
                </q-card-section>
                <q-card-actions align="center">
                  <q-btn flat style="color:rgba(39, 155, 72, 0.7)" @click="openArt">
                    <q-icon style="color:#474747" left size="3em" :name=name_art />
                    <div>MORE</div>
                  </q-btn>
                </q-card-actions>
              </q-card>
            </div>
          </div>

          <!-- content for prevention -->
          <div class="tm-icon">
            <div class="tm-icon-inner">
              <q-card class="my-card">
                <q-video src="https://www.youtube.com/embed/mJuHnfNorIg" />
                <q-card-section>
                  <div class="text-h4">Prevention</div>
                  <div class="text-subtitle2">Behavior and Tools</div>
                </q-card-section>
                <q-card-actions align="center">
                  <q-btn flat style="color:rgba(39, 155, 72, 0.7)" @click="openPrevention">
                    <q-icon style="color:#474747" left size="3em" :name=name_prevention />
                    <div>MORE</div>
                  </q-btn>
                </q-card-actions>
              </q-card>
            </div>
          </div>

        </div>
          <!-- ART -->
          <ART v-if="section == 'art'"/>
          <!-- Prevention -->
          <Prevention v-if="section == 'prevention'"/>
          <div v-if="section != null" class="q-pa-md, flex flex-center" style="height: 90px">
            <q-btn push color="accent" text-color="white" @click="scroll">
              <q-icon center flat size="3em" name="keyboard_arrow_up" />
              <div class="text-white"><strong>Back</strong></div>
            </q-btn>
          </div>
      </div>
    </q-page>
    <q-page>
      <subsession-title title="More funding is expected to meet fast-track HIV targets by 2030"/>
      <div class="q-pa-md">
        <expenditure/>
      </div>
    </q-page>
    <Source />
  </div>
</template>

<script>
import SessionBanner from "components/tools/SessionBanner";
import SubsessionTitle from "components/tools/SubsessionTitle";

import ART from "components/Actions/ART"
import Prevention from "components/Actions/Prevention"
import Expenditure from "components/Actions/Expenditure";

import Source from "components/Source"

export default {
name: "Conclusion",
  components: {Expenditure, SubsessionTitle, SessionBanner, ART, Prevention, Source},
  data() {
    return {
      section: null,
      show: false,
      name_art: "keyboard_arrow_up",
      name_prevention: "keyboard_arrow_up"
    }
  },
  methods: {
    onIntersection(entry) {
      // When the view intersects with the div, trigger animation to show the div content
      this.show = entry.isIntersecting
    },
    openArt(){
      // expand content when clicking on more
      if (this.section == null || this.section == 'prevention'){
        this.section = 'art'
        this.name_prevention = "keyboard_arrow_up"
        this.name_art = "keyboard_arrow_down"
      } else{
        this.section = null
        this.name_art = "keyboard_arrow_up"
      }
    },

    openPrevention(){
      // expand content when clicking on more
      if (this.section == null || this.section == 'art'){
        this.section = 'prevention'
        this.name_prevention = "keyboard_arrow_down"
        this.name_art = "keyboard_arrow_up"
      } else{
        this.section = null
        this.name_prevention = "keyboard_arrow_up"
      }
    },
    scroll() {
        const element = document.getElementById('ways');
        element.scrollIntoView({ behavior: 'smooth' });
    }
  }
}
</script>

<style scoped>
  .my-card{
    color: #644F3F;
  }
</style>
