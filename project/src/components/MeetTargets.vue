<template>
<!-- PART05: To Meet 2030 Goals: we should speed up to achieve the goals  -->
    <q-page>
      <session-banner img-url="images/meet_goal.jpg"
                        title="To Meet 2030 Goals"
                      subtitle="Although we have seen big success in controlling HIV/AIDS, the decreasing speed of new infections and deaths should be accelerated to achieve the goals."/>
      <div style="width:100%; padding:2%">
        <span style="font-size: 120%">Strong domestic and international commitment and funding for the AIDS response has fueled an acceleration of evidenced-based programs for prevention, testing and treatment.</span><br><br>
        <span style="font-size: 200%"><strong>However, this is well short of the progress set for 2020 milestones and required to meet 2030 3-zeros targets.</strong></span><br>
      </div>

       <div class="tm-row tm-social-row" style="margin:1%;padding:0px">
          <div class="tm-icon3">
              <q-card class="my-card, container" style="width:95%">
                <q-img src="images/card1.jpg" alt="art" class="image">
                  <div class="text-h5 absolute-bottom text-right">
                    Zero New Infections
                  </div>
                </q-img>
                <div class="overlay">
                  <div class="text" style="text-align:left;">
                    Despite the availability of this widening array of effective HIV prevention tools and methods and a massive scale-up of HIV treatment in recent years, new infections among adults globally have not decreased sufficiently. The 2016 United Nations Political Declaration on Ending AIDS target is to reduce new HIV infections to <strong>fewer than 500,000 by 2020</strong>, from more than 1.8 million in 2016. However, according to UNAIDS 2020 fact sheet, <strong>1.7 million</strong> are newly infected in 2020.<br>
                  </div>
                </div>
              </q-card>
          </div>

          <div class="tm-icon3">
              <q-card class="my-card, container" style="width:95%">
                <q-img src="images/card2.jpg" alt="art" class="image">
                  <div class="text-h5 absolute-bottom text-right">
                    Zero AIDS-Related Deaths
                  </div>
                </q-img>
                <div class="overlay">
                  <div class="text" style="text-align:left;">
                    AIDS-related deaths have been reduced by 60% since the peak in 2004 and AIDS-related mortality has declined by 39% since 2010. In 2019, around 690 000 people died from AIDS-related illnesses worldwide, compared to 1.7 million people in 2004 and 1.1 million people in 2010.<br>
                    HIV is marked as a disease that has multiple effective and relatively inexpensive treatment regimens available. The expanded access to HIV/AIDS related treatment has positive impact on decreasing the death rates in many regions.
                  </div>
                </div>
              </q-card>
          </div>

          <div class="tm-icon3">
              <q-card class="my-card, container" style="width:95%">
                <q-img src="images/card3.jpg" alt="art" class="image">
                  <div class="text-h5 absolute-bottom text-right">
                    Zero Discrimination
                  </div>
                </q-img>
                <div class="overlay">
                  <div class="text" style="text-align:left;">
                    The most recent data from population-based surveys show that, in 25 of 36 countries with recent data on a composite indicator that includes two types of discriminatory attitudes, more than 50% of people aged 15 to 49 years reported having discriminatory attitudes towards people living with HIV.<br>
                    There is a cyclical relationship between stigma and HIV; people who experience stigma and discrimination are marginalized. This makes them more vulnerable to HIV, while those living with HIV are more vulnerable to experiencing stigma and discrimination.
                  </div>
                </div>
              </q-card>
            </div>
          </div>
    </q-page>
</template>

<script>
import SessionBanner from "./tools/SessionBanner"

export default {
  name: "MeetTargets",
  components: {
    SessionBanner,
  }
}
</script>

<style  scoped>
  /* on hovering, shows text information over image card */
  .container {
    position: relative;
    width: 50%;
  }

  .image {
    display: block;
    width: 100%;
    height: auto;
  }

  .overlay {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%;
    width: 100%;
    opacity: 0;
    transition: .5s ease;
    background-color: rgba(45, 45, 45, 0.7);
  }

  .container:hover .overlay {
    opacity: 1;
  }

  .text {
    color: white;
    font-size: 18px;
    position: absolute;
    top: 50%;
    left: 50%;
    right: 0%;
    width: 90%;
    -webkit-transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    text-align: center;
  }
</style>
