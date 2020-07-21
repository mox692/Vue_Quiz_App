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
        
        <b-list-group>
            <b-list-group-item v-for="(item, index) in answers" :key="index" @click="clicked(index)">
              {{ index }}:{{ item }}
            </b-list-group-item>
        </b-list-group>
        answer:{{ currentQuestion.correct_answer }}



      </template>

      <hr class="my-4">

      <p>
        List of answear
      </p>

      <b-button variant="primary" href="#">submit</b-button>
      <b-button variant="success" href="#" @click="next">next</b-button>
    </b-jumbotron>
  </div>
</template>

<script src="lodash.js"></script>
       
<script>
import _ from 'lodash';
export default {
    // 親から渡ってきたcurrentQuestionを,props内で定義する
    props: {
        currentQuestion: Object,
        next: Function
    },
    data() {
      return {
        
      }
    },
    methods: {
      clicked(index) {
        alert(`${index} is clicked!`)
      }
    },
    computed: {
        answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        return answers
        }
    },
    watch: {
      //関数名が、そのままprops(or data)名
      currentQuestion() {
          var answer_array = this.currentQuestion.incorrect_answers.push(this.currentQuestion.correct_answer)
          console.log(this.currentQuestion.incorrect_answers)
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

</style>