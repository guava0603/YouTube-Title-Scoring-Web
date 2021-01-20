<template>
  <div id="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Banner />
    <Ranking />
    <!-- <Search v-if="currentTab === 0" @changeWeb="changeWeb" />
    <SearchedWord v-else :searchedData="resultData" @back="back"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Banner from '@/components/Banner.vue';
import Ranking from '@/components/Ranking.vue';
// import Search from '@/components/Search.vue'
// import SearchedWord from '@/components/SearchedWord.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld,
    Banner,
    Ranking
    // Search,
    // SearchedWord
  },
  data() {
    return {
      resultData: {},
      currentTab: 0
    }
  },
  methods: {
    changeWeb(resultData) {
      this.resultData = resultData;
      console.log(resultData);
      this.currentTab = 1;
    },
    back() {
      this.currentTab = 0;
    }
  }
}
</script>

<style scoped>
body {
  background: #f5f4f4;
}
#home {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  height: 100%;
}
</style>
