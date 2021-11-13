<template>
<!-- PART01: Starting Page -->
  <div>
    <q-page style="background-color:rgba(39, 155, 72, 0.8)">
      <div class="tm-row tm-about-row" style="height:65vh;">
        <div class="tm-section-1-r " style="width:50%;">
          <span class="text-white" style="font-size:400%">TOWARDS AN <br>HIV-FREE GENERATION.</span>
        </div>
        <div class="tm-section-1-l" style="width:50%; display:flex; margin:3%;">
          <span style="align-self:flex-end; front-size:200%"><h5 class="text-white"><strong>PROTECT AND ACCELERATE PROGRESS TOWARDS THE END OF AIDS: READY, SET, GO!</strong></h5></span>
        </div>
      </div>
      <div class="q-pa-md" style="height:10vx; margin-top:0px; display:flex; justify-content:center;">
        <div class="chevron" @click="scroll"></div>
        <div class="chevron" @click="scroll"></div>
    </div>
    </q-page>
  </div>
</template>

<script>
export default {
  name: "Intro",
  methods: {
    scroll() {
        const element = document.getElementById('start_session');
        element.scrollIntoView({ behavior: 'smooth' });
    }
  }
}
</script>

<style  scoped>
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    width: 100%;
    height: 100%;
    background: #333;
  }

  .chevron {
    position: absolute;
    width: 28px;
    height: 8px;
    opacity: 0;
    transform: scale3d(0.5, 0.5, 0.5);
    animation: move 3s ease-out infinite;
    cursor: pointer;
  }

  .chevron:first-child {
    animation: move 3s ease-out 1s infinite;
  }

  .chevron:nth-child(2) {
    animation: move 3s ease-out 2s infinite;
  }

  .chevron:before,
  .chevron:after {
    content: ' ';
    position: absolute;
    top: 0;
    height: 100%;
    width: 51%;
    background: #fff;
  }

  .chevron:before {
    left: 0;
    transform: skew(0deg, 30deg);
  }

  .chevron:after {
    right: 0;
    width: 50%;
    transform: skew(0deg, -30deg);
  }

  @keyframes move {
    25% {
      opacity: 1;

    }
    33% {
      opacity: 1;
      transform: translateY(30px);
    }
    67% {
      opacity: 1;
      transform: translateY(40px);
    }
    100% {
      opacity: 0;
      transform: translateY(55px) scale3d(0.5, 0.5, 0.5);
    }
  }

  .text {
    display: block;
    margin-top: 75px;
    margin-left: -30px;
    font-family: "Helvetica Neue", "Helvetica", Arial, sans-serif;
    font-size: 12px;
    color: #fff;
    text-transform: uppercase;
    white-space: nowrap;
    opacity: .25;
    animation: pulse 2s linear alternate infinite;
  }

  @keyframes pulse {
    to {
      opacity: 1;
    }
  }
</style>
