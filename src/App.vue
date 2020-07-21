<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
  <!-- 
    ・カスタム属性を定義している。
    ・子にデータを渡している。
    ・左辺のquestion,indexなどは、data内の変数として参照されている
   -->
    <Questionbox 
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
    />
  </div>
</template>
<script>
// ・App.vueはimportも含む。
// ・上のテンプレートで使用するVueオブジェクトはexport内で定義する。
import Questionbox from './components/Questionbox.vue'
export default {
  name: 'App',
  components: {
    Questionbox //外部テンプレートを読み込む場合。
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
  methods: {
    next: function(){
          this.index++;
      }
  },
  // loadした時にクイズを読み込む
  mounted: function(){
    let self = this
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
