<template>
  <div>
    <b-jumbotron>
      <template v-slot:header>QuizApp</template>

      <template v-slot:lead>
          <!-- 親から渡ってきたcurrentQuestionを受け取る -->
        question:{{ currentQuestion.question }}<br>
        answer:{{ currentQuestion.correct_answer }}
      </template>

      <hr class="my-4">

      <p>
        List of answear
      </p>

      <b-button variant="primary" href="#">submit</b-button>
      <b-button variant="success" href="#">next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
    
    props: {
        currentQuestion: Object
    }
}
</script>