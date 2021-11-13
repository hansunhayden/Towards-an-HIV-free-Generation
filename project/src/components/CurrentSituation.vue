<template>
<!--  PART03: Current Situation : Statistics of HIV/AIDS across the world -->
  <div>
    <SessionBanner
      img-url="images/current_situation2.jpg"
      title="Current Situation"
      subtitle="Global HIV/AIDS statistics"/>
    <div class="text-center text-h4 q-mt-xl q-mb-md">KEY NUMBERS ABOUT AIDS</div>
    <div class="center-div" style="max-width:1000px">
      <div class="text-body1 q-mb-md text-center">
        All the way through 1980s, we have seen the peak of infections in 2004. Now we are on the way to reduce new HIV infections, increase access to treatment and end AIDS-related deaths.
      </div>
    </div>
    <div class="row justify-evenly text-center" v-intersection="onIntersectionCounter">
      <div class="col-12 col-md-4">
        <NumberCounter number="1.7"
                       title="people were newly infected with HIV in 2019"
                       unit="million"
                       ref="counter1"
        />
      </div>
      <div class="col-12 col-md-4">
        <NumberCounter number="38"
                       title="people were living with HIV"
                       unit="million"
                       ref="counter2"
        />
      </div>
      <div class="col-12 col-md-4">
        <NumberCounter number="690"
                       title="people died of AIDS-related illness"
                       unit="thousand"
                       ref="counter3"
        />
      </div>
    </div>
    <!-- 3D globe for death rate and infection rate -->
    <GlobeViewLayout />

    <q-page>
        <SubsessionTitle title="HIV/AIDS New Infections"/>

        <section class="tm-mb-0 content-body">
          <div class="tm-row tm-about-row">
              <article class="tm-section-1-r">
                <br>
                <strong><span style="font-size:200%">1.7 million</span></strong> people became newly infected with HIV in 2019.<br>
                New HIV infections have been reduced by  <strong><span style="font-size:200%">40%</span></strong> since the peak in 1998 (2.8 million).
                <br>
                <br>
                <br>
                Since 2010, new HIV infections have declined by <strong><span style="font-size:120%">23%</span></strong>, from <strong><span style="font-size:120%">2.1</span></strong> million to <strong><span style="font-size:120%">1.7</span></strong> million in 2019.<br>
                Since 2010, new HIV infections among children have declined by <strong><span style="font-size:120%">52%</span></strong>, from <strong><span style="font-size:120%">310,000</span></strong> in 2010 to <strong><span style="font-size:120%">150,000</span></strong> in 2019.
              </article>
              <div class="tm-section-1-l" style="padding-top: 80px">
                  <NewInfections />
              </div>
          </div>
      </section>
    </q-page>

    <!-- world death content -->
    <q-page>
        <SubsessionTitle title="HIV/AIDS Related Deaths"/>

        <section class="tm-mb-0 content-body">
          <div class="tm-row tm-about-row">
              <article class="tm-section-1-r">
                <br>
                AIDS-related deaths have been reduced by <strong><span style="font-size:200%">60%</span></strong> since the peak in 2004, and <strong><span style="font-size:200%">39%</span></strong> since 2010.<br><br>
                In 2019, around <strong><span style="font-size:200%">690,000</span></strong> people died from AIDS-related illnesses worldwide, compared to <strong><span style="font-size:120%">1.1</span></strong> million people in 2010.<br>
              </article>
              <div class="tm-section-1-l" style="padding-top: 80px">
                  <WorldDeathRace />
              </div>
          </div>
      </section>
    </q-page>

    <!-- world key population content -->
    <q-page>
      <SubsessionTitle title="HIV/AIDS Among Key Populations"/>

      <section class="tm-mb-0 content-body">
        <div class="tm-row tm-about-row" v-intersection.once="onIntersection">
          <transition class="fade-in-text">
            <article v-if="show" class="tm-section-1-r">
              <br>
              The RISK OF AQUIRING HIV IS:
              <br>
              <br>
              <ul>
              <li> <strong><span style="font-size:200%">26</span></strong> times higher among <span style="color: #B15057;font-size:120%"><strong> men and other men who have sex with men</strong></span></li>
              <li> <strong><span style="font-size:200%">29</span></strong> times higher among <span style="color: #AEAC70;font-size:120%"><strong> who inject drugs</strong></span></li>
              <li> <strong><span style="font-size:200%">30</span></strong> times higher for <span style="color: #B19287;font-size:120%"><strong> sex workers</strong></span></li>
              <li> <strong><span style="font-size:200%">13</span></strong> times higher for <span style="color:#0E5D54;font-size:120%"><strong> transgender people</strong></span></li>
              </ul>
            </article>
            </transition>
            <div class="tm-section-1-l" style="padding-top: 80px">
              <AmongKeyPop />
            </div>
        </div>
      </section>
    </q-page>
  </div>
</template>

<script>
import SessionBanner from "./tools/SessionBanner"
import SubsessionTitle from "./tools/SubsessionTitle"

import NewInfections from "components/CurrentSituation/NewInfections"
import WorldDeathRace from "components/CurrentSituation/WorldDeathRace"
import AmongKeyPop from "components/CurrentSituation/AmongKeyPop"
import GlobeViewLayout from "components/CurrentSituation/GlobeGLComponent/GlobeViewLayout";
import NumberCounter from "components/tools/NumberCounter";

export default {
  name: 'CurrentSituation',
  components: {
    NumberCounter,
    SessionBanner,
    SubsessionTitle,
    GlobeViewLayout,
    NewInfections,
    WorldDeathRace,
    AmongKeyPop
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
    onIntersectionCounter(){
      // When the view intersects with the div, trigger animation of number counter
      this.$refs.counter1.startAnim();
      this.$refs.counter2.startAnim();
      this.$refs.counter3.startAnim();
    }
  },
};
</script>
