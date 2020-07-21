<template>
  <div>
    <b-jumbotron>
      <template v-slot:header>QuizApp</template>
      <template v-slot:lead>
         
          <!-- 
              ・親から渡ってきたcurrentQuestionを受け取る
              ・他のコンポーネント(この場合は親)で定義されたdataにもアクセスできる
          -->
        question:{{ currentQuestion.question }}<br>
        answer:{{ currentQuestion.correct_answer }}
      </template>
      <hr class="my-4">
      <Header
        :correctAnswers="correctAnswers"
        :submittedQuestion="submittedQuestion"
          />
      <p>
        <b-list-group>
            <b-list-group-item v-for="(item, index) in shuffledAnswer" :key="index" @click="clicked(index)">
              {{ index }}:{{ item }}
            </b-list-group-item>
        </b-list-group>
      </p>
      
  
      <b-button 
        variant="primary" 
        class="submit-button"
        @click="submitted(clickedAnswer)"
        :disabled="isSubmitted"
        >submit
      </b-button>
      <b-button 
        variant="success" 
        @click="next" 
        :disabled="!isSubmitted"
        class="submit-button"
      >next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script src="lodash.js"></script>
       
<script>
import _ from 'lodash';
import Header from './Header.vue'
export default {

    components: {
      Header
    },
    // 親から渡ってきたcurrentQuestionを,props内で定義する
    props: {
        currentQuestion: Object,
        next: Function
    },
    data() {
      return {
        shuffledAnswer: [],
        clickedAnswer: 0,
        correctAnswers: 0,
        submittedQuestion: 0,
        isClicked: false,
        isSubmitted: false
      }
    },
    methods: {
      clicked(index) {
        this.clickedAnswer =  index
        this.isClicked = true
      },
      submitted(clickedAnswer){
        console.log(Object.values(this.shuffledAnswer[this.clickedAnswer]))
        if(this.shuffledAnswer[this.clickedAnswer] == this.currentQuestion.correct_answer){
          alert("good job!!")
          this.correctAnswers++
          this.$parent.correctAnswers = this.correctAnswers
          
          // console.log(this.correctAnswers)
        }
        else{
          alert('oh...')
        }
        this.isSubmitted = true
        this.submittedQuestion++
        // console.log(correctAnswers)
      }
    },
    computed: {
        answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        // answers.push(this.currentQuestion.correct_answer)
        
        return answers
        }
    },
    watch: {
      //関数名が、そのままprops(or data)名
      currentQuestion : {
        immediate: true,
        handler() {
            var answer_array = this.currentQuestion.incorrect_answers.push(this.currentQuestion.correct_answer)
            //なぜかこっちがうまくいく。。。。。
            this.isSubmitted = false
            this.shuffledAnswer = _.shuffle(this.currentQuestion.incorrect_answers)
                  }
      }
    },
    mounted(){
     
    } 
}
</script>

<style scoped>
ul{
    list-style-type: none;
}
.list-group-item:hover{
    background-color: #c9c9c9;
    cursor : pointer;
}
.clicked{
  background-color: pink;
}
.submit-button{
  display: block;
  width: 100px;
  font-size: 1.2rem;
  margin: 0 auto 10px auto;
  /* padding-bottom: 20px; */
}
</style>