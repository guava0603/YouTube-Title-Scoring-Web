<template>
  <!-- app -->
  <div id="banner-outer">
    <div id="banner">
      <div class="reverse">YouTube</div>
      <span>Title Scoring</span>
    </div>
    <div id="banner-line">
    </div>
  </div>
</template>

<script>
// import $ from 'jquery';
// import { TimelineMax, Back, Expo, Power4 } from "gsap";


export default {
  name: 'Bannner',
  data() {
    return {
      state: {
        apiResults: null,
        results: [],
        keyword: '',
        resultsMode: false
      },
      ENDPOINT: '//en.wikipedia.org/w/api.php'
    }
  },
  computed: {
    resultsMode() {
      return this.state.resultsMode;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$c-gold: #FEDC3D;
$c-peach: #FEA680;
$c-azure: #02ACAB;

$c-1: #1E2649;
$c-1-l: #9B8DE5;
$c-2: #F66760;
$c-2-l: #F9A1A0;

$c-bg: $c-1;

@keyframes banner_pos {
  0% {
    transform: translateX(-110vw);
  } 50% {
    transform: translateX(-110vw);
  } 92% {
    transform: translateX(0vw);
  } 95% {
    transform: translateX(-0.5vw);
  } 100% {
    transform: translateX(0);
  }
}

@keyframes banner_pos_reverse {
  0% {
    transform: translateX(100vw);
  } 100% {
    transform: translateX(0);
  }
}

#banner-outer {
  width: 100%;
}

#banner {
  background: white;
  width: 100vw;
  box-shadow: 2px 4px 10px -6px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  padding: 3vw 5vw;
  animation-name: banner_pos;
  animation-timing-function: ease;
  // transform: translateX(-100vw);
  animation-duration: 2s;
  span {
    color: #c4302b;
    font-weight: 900;
    font-size: 200%;
    transition: all, 2s;
  }
  .reverse {
    background: #c4302b;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
    font-weight: 900;
    font-size: 200%;
    padding: 3px 10px;
    margin: 0 10px;
  }
}
#banner-line {
  margin-top: 10px;
  width: 100%;
  height: 15px;
  background: white;
  box-shadow: 2px 4px 10px -6px rgba(0, 0, 0, 0.2);
  animation-name: banner_pos_reverse;
  animation-timing-function: ease-out;
  animation-duration: 1s;
}
</style>
