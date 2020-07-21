<template>
  <div id="app">

  <!-- 
    ・カスタム属性を定義している。
    ・子にデータを渡している。
    ・左辺のquestion,indexなどは、data内の変数として参照されている
   -->
    <Titlepage
      v-if="displayHome"
    />

    <!-- <input type="button" @click="startQuiz"> -->
    <b-button 
      v-if="displayHome  && index < 9"
      variant="info" 
      class="start-button" 
      @click="startQuiz"
      style="font-size:1.8rem;"
    >
    Let's Start
    </b-button>

    <Questionbox 
      v-if="questions.length && displayQuiz && index < 9"
      :currentQuestion="questions[index]"
      :next="next"
      :submittedQuestion="submittedQuestion"
    />

    <Endingpage
      v-if="index==9"
      :correctAnswers="correctAnswers"
    />
  </div>
</template>
<script>
// ・App.vueはimportも含む。
// ・上のテンプレートで使用するVueオブジェクトはexport内で定義する。
import Questionbox from './components/Questionbox.vue'
import Titlepage from './components/Titlepage.vue'
import Endingpage from './components/Endingpage.vue'
export default {
  name: 'App',
  components: {
    Questionbox, //外部テンプレートを読み込む場合。
    Titlepage,
    Endingpage
  },
  data() {
    return {
      questions: [],
      index: 0,
      correctAnswers: 0,
      submittedQuestion: 0,
      displayQuiz: false,
      displayHome: true,
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
      },
    startQuiz(){
      this.displayQuiz = true
      this.displayHome = false
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

.start-button{
  width: 200px;
  font-size: 2rem;
}
</style>
