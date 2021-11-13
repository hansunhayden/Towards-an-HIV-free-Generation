<template>
  <div class="q-pa-md" style="background-color:#3A3A3A; height: 70px; margin-top:0px; display:flex; justify-content:center;">
    <q-btn @click="scroll" push align="around"  text-color="white" label="Source" icon="lightbulb_outline" style="margin:auto; display:block; background:#4B4B4B;"/>
  </div>

  <div class="row" style="background-color:#3A3A3A;" v-if="show" id="source">
    <div class="column">
      <p>
        <span style="color:whitesmoke; font-size:120%">Data Source:</span><br>
        Our World in Data: <a href="https://ourworldindata.org/hiv-aids">https://ourworldindata.org/hiv-aids</a><br>
        UNAIDS: <a href="http://aidsinfo.unaids.org/">http://aidsinfo.unaids.org/</a><br>
        statista: <a href="https://www.statista.com/topics/773/hiv-aids-worldwide/">https://www.statista.com/topics/773/hiv-aids-worldwide/</a>
      </p>
    </div>
    <q-separator vertical inset color="white"/>
    <div class="column">
       <p>
        <span style="color:whitesmoke; font-size:120%">Software:</span><br>
        Data Processing: <a href="https://pandas.pydata.org/">Pandas</a>, <a href="https://geopandas.org/">GeoPandas</a><br>
        Front-end design and development: <a href="https://v3.vuejs.org/">Vue</a>, <a href="https://quasar.dev/">Quasar</a>, <a href="https://animejs.com/">animejs</a><br>
        Visualization: <a href="https://docs.mapbox.com/mapbox-gl-js/api/">Mapbox</a>, <a href="https://globe.gl/">Globe.GL</a>, <a href="https://d3js.org/">D3.js</a>, <a href="https://echarts.apache.org/zh/index.html">Apache ECharts</a>
      </p>
    </div>
    <q-separator vertical inset color="white"/>
    <div class="column">
      <p>
        <span style="color:whitesmoke; font-size:120%">Images: </span><br>
        Website Icon from World AIDS Day Pack on: <a target="_blank" href="https://www.flaticon.com/">Flaticon</a><br/>
        All Menu Icons from: <a target="_blank" href="https://fonts.google.com/icons?selected=Material+Icons">Google Material Design Icons</a><br/>
        All Image sources are listed <button class="help" @click="help">here</button>
      </p>
    </div>
    <div v-show="maskShow">
      <div class="mask"></div>
      <div class="info-box">
        <div class="info">
          <div style="padding:12px">
            <div style="font-weight: bold;">Image Resources Listed in the Order of Appearance on the Website:</div>
            <div>
              <br/>
              <strong>Silence = Death banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/</a> <br/>

              <strong>History of HIV/AIDS Spread:</strong> <a class="image_source" target="_blank" href="https://www.gettyimages.co.uk/detail/news-photo/patron-looks-at-silencedeath-project-during-an-exhibition-news-photo/1035373318?adppopup=true">https://www.gettyimages.co.uk/detail/news-photo/patron-looks-at-silencedeath-project-during-an-exhibition-news-photo/1035373318?adppopup=true </a> <br/>

              <strong>Silence = Death poster:</strong> <a class="image_source" target="_blank" href="https://www.brooklynmuseum.org/opencollection/objects/159258">https://www.brooklynmuseum.org/opencollection/objects/159258 </a> <br/>

              <strong>Silence = Death Parade:</strong> <a class="image_source" target="_blank" href="https://www.gettyimages.co.uk/detail/news-photo/patron-looks-at-silencedeath-project-during-an-exhibition-news-photo/1035373318?adppopup=true">https://www.gettyimages.co.uk/detail/news-photo/patron-looks-at-silencedeath-project-during-an-exhibition-news-photo/1035373318?adppopup=true </a> <br/>

              <strong>Current Situation Banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a> <br/>

              <strong>Sustainable Development Goals Banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a> <br/>

              <strong>Heterogeneous Distribution Banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a> <br/>

              <strong>Inequality between genders:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a> <br/>

              <strong>To Meet 2030 Goals Banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a> <br/>

              <strong>3 Zero Targets:</strong> <a class="image_source" target="_blank" href="https://www.pexels.com/zh-cn/">https://www.pexels.com/zh-cn/ </a> <br/>

              <strong>Take Actions Banner:</strong> <a class="image_source" target="_blank" href="https://hlm2021aids.unaids.org/">https://hlm2021aids.unaids.org/ </a><br/>
            </div>
            <div class="hr" style="margin:10px 0px"></div>
            <button style="width: 55px;float: right;" @click="close">
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- <div class="text-body2 q-pl-lg q-pr-lg q-pb-sm">
    &copy; 2021 Han Sun & Jingyan Li. All rights reserved.
  </div> -->


</template>

<script>
export default {
  name: "Source",
  data() {
    return {
      show: false,
      maskShow: false
    }
  },
  methods: {
    scroll() {
      if (this.show == true) {
        this.show = false
      }else{
        this.show = true
        setTimeout(() => {
          const element = document.getElementById('source');
          element.scrollIntoView({ behavior: 'smooth' });
        }, 100)
      }
    },
    help() {
      this.maskShow = true;
    },
    close() {
      this.maskShow = false;
    },
  },
}
</script>

<style  scoped>
  .column {
    float: left;
    width: 33%;
    padding-left: 2%;
    color: #D2D2D2;
  }

  .row:after {
    content: "";
    display: table;
    clear: both;
  }

  .no_underline {
    text-decoration: none;
  }

  p {
    color: #D2D2D2;
    font-size: 90%;
  }

  a {
    color: #D2D2D2;
    text-decoration: underline;
    font-size: 80%;
  }

  html {
    scroll-behavior: smooth;
  }

  .mask {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1000;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.45);
  }
  .info-box {
    position: fixed;
    top: 100px;
    left: 0px;
    width: 100%;
    z-index: 1001;
  }
  .info {
    width: 900px;
    height: 420px;
    margin: auto;
    background-color: #76BF8A;
    opacity: 0.95;
    font-size: 16px;
  }
  .image_source {
    color: #474747;
    text-decoration: underline;
    font-size: 80%;
  }

  @media screen and (max-width: 600px) {
    .column {
      width: 100%;
    }
  }
</style>
