<template>
  <SubsessionTitle title="HIV/AIDS Prevention" />
  <div>
    <h6 style="margin:1%">
      <br>
      <span style="font-size:140%">No single prevention method or approach can stop the HIV epidemic on its own</span>. Several methods and interventions have proved highly effective in preventing HIV infection.<br><br>
      Recent years, progress in HIV research provides effective HIV prevention tools. For people who are at high risk of getting HIV, medical tools like <span style="font-size:140%">PrEP and PEP</span> could be used to effectively reduce the risk of getting infected.
    </h6>
  </div>
  <q-page>
    <section class="tm-mb-0 content-body">
        <div class="tm-row tm-about-row"> 

          <!-- content for PrEP -->
          <div class="tm-section-1-l, q-pa-md" style="width:50%;">
              <q-video src="https://www.youtube.com/embed/nnF_Xko1hFs"
                style="margin-top:1%; width:100%"/>
              <q-stepper
                v-model="step"
                vertical
                color="primary"
                animated
              >
                <q-step
                  :name="1"
                  title="What is PrEP?"
                  icon="add_comment"
                  :done="step > 1"
                >
                  PrEP (pre-exposure prophylaxis) is medicine people at risk for HIV take to prevent getting HIV from sex or injection drug use.
                  <br>
                  PrEP is safe but some people experience side effects like diarrhea, nausea, headache, fatigue, and stomach pain. These side effects usually go away over time.
                  <q-stepper-navigation>
                    <q-btn @click="step = 2" color="primary" label="Continue" />
                  </q-stepper-navigation>
                </q-step>

                <q-step
                  :name="2"
                  title="What is PrEP?"
                  icon="add_comment"
                  :done="step > 2"
                >
                  The proposed recommendations, recently released by the task force, concluded that pre-exposure prophylaxis (PrEP), a daily pill that helps prevent contracting HIV, can be little-used for anyone who has sex with a partner who has the virus, anyone who has condomless sex with a partner whose status is unknown, and those who share injection drug or tattoo needles.Separately, the task force also proposed that doctors screen patients who are 15 to 65 years old for HIV.
                  <q-stepper-navigation>
                    <q-btn @click="step = 3" color="primary" label="Continue" />
                    <q-btn flat @click="step = 1" color="primary" label="Back" class="q-ml-sm" />
                  </q-stepper-navigation>
                </q-step>

                <q-step
                  :name="3"
                  title="PrEP Effectiveness"
                  icon="add_comment"
                >
                  <span style="font-size: 120%;">PrEP is highly effective for preventing HIV.</span>
                  <ul>
                    <li>PrEP reduces the risk of getting HIV from sex by about 99% when taken as prescribed</li>
                    <li> Although there is less information about how effective PrEP is among people who inject drugs, we do know that PrEP reduces the risk of getting HIV by at least 74% when taken as prescribed</li>
                  </ul>
                  <q-stepper-navigation>
                    <q-btn color="primary" label="Finish" />
                    <q-btn flat @click="step = 2" color="primary" label="Back" class="q-ml-sm" />
                  </q-stepper-navigation>
                </q-step>
              </q-stepper>
          </div>

          <!-- content for PEP -->
          <div class="tm-section-1-r, q-pa-md" style="width:50%">
              <q-video src="https://www.youtube.com/embed/Yu82TFo6j94"  
              style="margin-top:1%; width:100%"/>
            <q-stepper
              v-model="step2"
              vertical
              color="primary"
              animated
            >
              <q-step
                :name="4"
                title="What is PEP?"
                icon="add_comment"
                :done="step2 > 4"
              >
                PEP (post-exposure prophylaxis) means taking medicine to prevent HIV after a possible exposure.
                <br>
                PEP Must Be Started Within 72 Hours of Possible Exposure to HIV.
                The sooner you start PEP, the better. Every hour counts. If you’re prescribed PEP, you’ll need to take it daily for 28 days.
                <q-stepper-navigation>
                  <q-btn @click="step2 = 5" color="primary" label="Continue" />
                </q-stepper-navigation>
              </q-step>

              <q-step
                :name="5"
                title="Who is PEP for?"
                icon="add_comment"
                :done="step > 5"
              >
                <span style="font-size: 120%;">PEP is for Emergency Situations</span>
                <ul>
                  <li>PEP is given after a possible exposure to HIV</li>
                  <li>PEP is not a substitute for regular use of other HIV prevention</li>
                  <li>PEP is not the right choice for people who may be exposed to HIV frequently</li>
                  <li>If you are at ongoing risk for HIV, such as through repeated exposures to HIV, talk to your health care provider about PrEP (pre-exposure prophylaxis)</li>
                </ul>
                <q-stepper-navigation>
                  <q-btn @click="step2 = 6" color="primary" label="Continue" />
                  <q-btn flat @click="step2 = 4" color="primary" label="Back" class="q-ml-sm" />
                </q-stepper-navigation>
              </q-step>

              <q-step
                :name="6"
                title="PEP Effectiveness"
                icon="add_comment"
              >
                If taken within 72 hours after possible exposure, PEP is highly effective in preventing HIV. But to be safe, you should take other actions to protect your partners while you are taking PEP. <br>
                PEP is safe but may cause side effects like nausea in some people. In almost all cases, these side effects can be treated and aren’t life-threatening.
                <q-stepper-navigation>
                  <q-btn color="primary" label="Finish" />
                  <q-btn flat @click="step2 = 5" color="primary" label="Back" class="q-ml-sm" />
                </q-stepper-navigation>
              </q-step>
            </q-stepper>
          </div>

        </div>
    </section>
  </q-page>
</template>

<script>
import SubsessionTitle from "../tools/SubsessionTitle"

export default {
  name: "Prevention",
  components: {
    SubsessionTitle
  },
  data() {
    return {
      step: 1,
      step2:4
    }
  },
}
</script>

<style  scoped>

</style>
