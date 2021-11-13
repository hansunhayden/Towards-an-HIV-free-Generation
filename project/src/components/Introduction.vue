<template>
<!-- PART02: Silence = Death : History of HIV/AIDS-->
  <div>
    <Intro />
    <SessionBanner
      img-url="images/Actup-13.jpg"
      title="Silence = Death"
      subtitle="Since the breakout of HIV/AIDS"
      id="start_session"/>

    <div class="tm-row tm-about-row">
      <div class="tm-section-1-l" style="text-align:left; width:60%; padding-top:5%; padding-left:2%">
        <q-timeline color="secondary">
          <q-timeline-entry heading>
            <h4>History of HIV/AIDS Spread</h4>
          </q-timeline-entry>

          <q-timeline-entry
            title="Begin of AIDS Epidemic"
            subtitle="Year 1981"
            icon="theaters"
          >
            <div>
              The AIDS epidemic officially began on June 5, 1981, when the U.S. Centers for Disease Control and Prevention reported unusual clusters of Pneumocystis pneumonia (PCP).<br>
            </div>
          </q-timeline-entry>

          <q-timeline-entry
            title="GRID TO AIDS"
            subtitle="Year 1982"
            icon="theaters"
          >
            <div>
              In June 1982, a report of a group of cases amongst gay men in Southern California suggested that a sexually transmitted infectious agent might be the etiological agent.The syndrome was initially termed "GRID".<br>
              By August 1982, the disease was being referred to by its new CDC-coined name: Acquired Immune Deficiency Syndrome (AIDS).
            </div>
          </q-timeline-entry>
          <q-timeline-entry>
          </q-timeline-entry>
        </q-timeline>
      </div>
      <div class="tm-section-1-r" style="width:47%; display:flex; justify-content:center;">
        <div class="getty embed image" style="background-color:#fff;display:inline-block;font-family:Roboto,sans-serif;color:#a7a7a7;font-size:11px;width:100%;max-width:594px;">
          <div style="padding:0;margin:0;text-align:left;">
            <a href="http://www.gettyimages.co.uk/detail/1035373318" target="_blank" style="color:#a7a7a7;text-decoration:none;font-weight:normal !important;border:none;display:inline-block;">
              Embed from Getty Images
            </a>
          </div>
          <div style="overflow:hidden;position:relative;height:0;padding:69.19192% 0 0 0;width:100%;">
            <iframe src="//embed.gettyimages.com/embed/1035373318?et=IcMyB5aRR0NwLiJczvnUxQ&tld=co.uk&sig=d4Y_sMQN7tolFrSBtzASvk8zIrBl65rhd1Lg9JiD3iE=&caption=true&ver=1" scrolling="no" frameborder="0" width="594" height="411" style="display:inline-block;position:absolute;top:0;left:0;width:100%;height:100%;margin:0;">
            </iframe>
          </div>
        </div>
     <!--        <img src="images/aids_research.jpg" style="width:100%; margin:auto; display:block"/>-->
      </div>
    </div>

    <div class="q-pa-md row items-start q-gutter-md">
      <q-card class="my-card" flat bordered>
        <q-card-section horizontal>
          <q-card-section class="q-pt-xs">
            <div class="text-overline">Gain Public Attention</div>
            <div class="text-h5 q-mt-sm q-mb-xs">Silence = Death</div>
            <div style="padding-right:5%">
              <br>
              At the beginning of the AIDS epidemic in the 1980s, there was very little information about the disease. Also, because AIDS affected stigmatized groups, such as LGBTQ and people of low socioeconomic status, there wasn't much mass media coverage initially when the epidemic started. However, with the rise of activist groups composed of people suffering from AIDS, either directly or through a loved one, more public attention was brought to the epidemic.
            </div>
          </q-card-section>

          <q-card-section class="col-2 flex flex-center">
            <q-img
              class="rounded-borders"
              src="images/silenceDeath.jpg"
            />
          </q-card-section>
        </q-card-section>
      </q-card>
    </div>

    <div class="tm-row tm-about-row">
      <div class="tm-section-1-l" style="text-align:left; width:65%; padding-top:3%; padding-left:2%">
        <i style="color:#6D6D6D; "> 1987, Avram Finkelstein, Brian Howard, Oliver Johnston, Charles Kreloff, Chris Lione, and Jorge Socarrás founded the SILENCE=DEATH Project to support one another in the midst of the AIDS crisis. Inspired by the posters of the Art Workers Coalition and the Guerrilla Girls (both of whose work is on view nearby), they mobilized to spread the word about the epidemic and created the now-iconic Silence=Death poster featuring the pink triangle as a reference to Nazi persecution of LGBTQ people in the 1930s and 1940s. </i><br><br>
        This design became the central visual symbol of AIDS activism after it was adopted by the direct action advocacy group AIDS Coalition to Unleash Power (ACT UP).
      </div>
      <div class="tm-section-1-r" style="width:30%;">
        <div class="getty embed image" style="background-color:#fff;display:inline-block;font-family:Roboto,sans-serif;color:#a7a7a7;font-size:11px;width:100%;max-width:594px;"><div style="padding:0;margin:0;text-align:left;"><a href="http://www.gettyimages.co.uk/detail/1213566318" target="_blank" style="color:#a7a7a7;text-decoration:none;font-weight:normal !important;border:none;display:inline-block;">Embed from Getty Images</a></div><div style="overflow:hidden;position:relative;height:0;padding:69.36027% 0 0 0;width:100%;"><iframe src="//embed.gettyimages.com/embed/1213566318?et=DDbMbPdqQr1T7pOi8geEvA&tld=co.uk&sig=oWI0HUjRHSjVvlld7kiW-3Ehfm4wZwOTwYJlAvIw0Ks=&caption=true&ver=1" scrolling="no" frameborder="0" width="594" height="412" style="display:inline-block;position:absolute;top:0;left:0;width:100%;height:100%;margin:0;"></iframe></div></div>
<!--        <img src="images/public.jpg" style="width:100%;" />-->
      </div>
    </div>

    <div v-intersection.once="onIntersection" class="q-pa-md" style="margin-top:0px;">
      <transition class="fade-in-text">
        <div v-if="show" id="slogan" style="text-align: center; font-size: 150%; color:#5A5A5A">
          In recent decades, major global efforts have been mounted to address the epidemic, and despite challenges, significant progress has been made in addressing HIV.
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import SessionBanner from './tools/SessionBanner'
import Intro from './Intro'


export default {
  name: 'Introduction',
  components: {
    SessionBanner,
    Intro
  },
  data() {
    return {
      show: false
    }
  },
  methods: {
    onIntersection(entry) {
      // When the view intersects with the div, trigger animation to show the div content
      this.show = entry.isIntersecting
    }
  },
};
</script>

<style scoped>
  #slogan{
      padding: 25px;
      max-width: 100%;
      text-align: center;
      position: relative;
  }
  #slogan:before,
  #slogan:after{
      position: absolute;
      font-size: 50px;
      color: #2b2828;
      font-weight: 700;
  }
  #slogan:before{
      content: '\201c';
      top: 0; left: 10px;
  }
  #slogan:after{
      content: '\201d';
      bottom: 0; right: 10px;
  }
</style>
