<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <Questionbox 
      :currentQuestion="questions[index]"
    />
  </div>
</template>

<script>

import Questionbox from './components/Questionbox.vue'

export default {
  name: 'App',
  components: {
    Questionbox
  },
  data() {
    return {
      questions: [],
      index: 0,
      user: [
        {
          name: "元幸",
          age: 23
        },
        {
          name: "幸子",
          age:33
        }
      ]
    }
  },
  // loadした時にクイズを読み込む
  mounted: function(){
    let self = this
    console.log(this.questions);
    fetch('https://opentdb.com/api.php?amount=10&category=18')
    .then(function(response) {
      return response.json();
    })
    .then(function(myJson) {
      self.questions = myJson.results;
    });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
