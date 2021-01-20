<template>
  <!-- app -->
  <div id="ranking-outer">
    <div class="title-block" v-for="(title, idx) in titles" :key="idx">
      <div class="title">
        <span>{{ title[0] }}</span>
        <div v-if="recommended_id === idx" class="success">
          <div v-for="recom in recommended" :key="recom" class="success-block">
            {{ recom }}
          </div>
        </div>
      </div>
      <div class="score">
        <span>{{ title[1] }}</span>
        <div @click="getTitle(idx, title[0])" class="button">recomm</div>
      </div>
    </div>
    <AddButton @addTitle="addTitle" />
  </div>
</template>

<script>
import $ from 'jquery';
import AddButton from './AddButton.vue';
// import $ from 'jquery';
// import { TimelineMax, Back, Expo, Power4 } from "gsap";


export default {
  components: { AddButton },
  name: 'Bannner',
  data() {
    return {
      recommended_id: -1,
      recommended: [],
      titles: [],
      state: {
        apiResults: null,
        results: [],
        keyword: '',
        resultsMode: false
      },
      ENDPOINT: '//en.wikipedia.org/w/api.php'
    }
  },
  methods: {
    addTitle(item) {
      this.titles.push(item);
      this.titles.sort((a, b) => b[1]-a[1]);
      this.recommended_id = -1;
      console.log('addTitle', this.titles);
    },
    getTitle(idx, title) {
      let a = '';
      $.ajax({
          url: `http://localhost:5000/article/${title}`,
          dataType: 'json',
          success: res => {
            this.state.results = res;
            this.recommended = res.data;
            this.recommended_id = idx;
            console.log(res.data);
            //this.$emit('addTitle', [this.newTitle, res])
            //this.isClick = false;
            //this.newTitle = '';
          }
        })
      console.log('a', a);
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
#ranking-outer {
  margin-top: 5vh;
  width: 50vw;
  min-height: 60vw;
  border: 3px dotted #f6ecf0;
  box-shadow: 2px 4px 10px -6px rgba(0, 0, 0, 0.2);
  background: white;
  border-radius: 5vw;
  padding: 3vw;
  overflow-y: scroll;

  display: flex;
  flex-direction: column;
  align-items: center;
}
.title-block {
  padding: 5px;
  width: 80%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  box-shadow: 2px 4px 10px -6px #f6ecf0;
  margin: 2vw;
  font-weight: 800;
  align-items: flex-start;
  .button {
    cursor: pointer;
    color: gray;
    border-radius: 5px;
    font-size: 10px;
    :hover {
      background: #aaaaaa;
      padding: 3px;
      }
  }
}

.score {
  max-width: 40%;
}

.title {
  display: flex;
    flex-direction: column;
  align-items: flex-start;
  }

.success-block {
  color: gray;
  font-size: 12px;
  padding: 5px;
  text-align: left;
  padding-left: 0;
}
</style>
