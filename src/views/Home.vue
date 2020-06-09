<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Search v-if="currentTab === 0" @changeWeb="changeWeb" />
    <SearchedWord v-else :searchedData="resultData" @back="back"/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Search from '@/components/Search.vue'
import SearchedWord from '@/components/SearchedWord.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld,
    Search,
    SearchedWord
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
