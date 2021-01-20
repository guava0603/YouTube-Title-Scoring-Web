<template>
  <!-- app -->
  <div id="add-button" @keydown.enter="submit">
    <img v-if="!isClick" class="add" @click="isClick=true" src="../assets/plus.svg">
    <div v-if="!isClick" class="click-me">
      <span>Click me!</span>
      <div class="tail"></div>
    </div>
    <input v-if="isClick" placeholder="Input your title" class="text" v-model="newTitle" />
    <img v-if="isClick" class="cancel" @click="isClick=false" src="../assets/ic_delete.svg">
  </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: 'Add',
  data() {
    return {
      state: {
        apiResults: null,
        results: [],
        keyword: '',
        resultsMode: false
      },
      newTitle: '',
      isClick: false
    }
  },
  computed: {
    resultsMode() {
      return this.state.resultsMode;
    }
  },
  methods: {
    submit() {
      if (this.newTitle) {
        // const vm = this;
        $.ajax({
          url: `http://localhost:5000/search/${this.newTitle}`,
          dataType: 'json',
          success: res => {
            // this.state.results = res;
            this.$emit('addTitle', [this.newTitle, res])
            this.isClick = false;
            this.newTitle = '';
          }
        })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@keyframes rotate_button {
  0% {
    transform: rotate(0);
  } 6% {
    transform: rotate(10deg);
  } 12% {
    transform: rotate(-10deg);
  } 20% {
    transform: rotate(0);
  }
}

@keyframes display_font {
  0% {
    opacity: 1;
  } 20% {
    opacity: 1;
  } 40% {
    opacity: 0;
  } 90% {
    opacity: 0;
  }
}

#add-button {
  position: relative;
  margin-top: 10px;
  // top: 30vh;
  // left: 10px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  img.add {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background: white;
    box-shadow: 2px 4px 10px -6px rgba(0, 0, 0, 0.2);
    animation: rotate_button 5s infinite;
  }
  .click-me {
    position: absolute;
    top: -30px;
    right: -30px;
    padding: 3px 5px;
    background: white;
    font-size: 14px;
    border-radius: 4px;
    animation: display_font 3s infinite;
    // box-shadow: 2px 4px 10px -6px #cd5d7d;
    font-weight: 700;
    color: white;
    background: #f1d4d4;
    .tail {
      position: absolute;
      width: 0;
      height: 0;
      border-style: solid;
      border-width: 12px 5px 0 5px;
      border-color: #f1d4d4 transparent transparent transparent;
      transform: translateX(7px);
    }
  }
}

input.text {
  width: 200px;
  height: 40px;
  margin-left: -100px;
  border: none;
  // box-shadow: 2px 4px 10px -6px rgba(0, 0, 0, 0.6);
  outline: none;
  padding: 0 5px;
  background: #f4f4f4;
  font-weight: 700;
  border: 3px solid #f0f0f0;
  :placeholder {
    color: #eeeeee;
  }
}
img.cancel {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  transform: translateY(-50px) translateX(90px);
  border: 2px solid rgba(0, 0, 0, 0.1);
}
</style>
