<template>
<div>
    <p>{{ this.correctAnswers }}/{{ this.submittedQuestion }}</p>
</div>

</template>
<script>
export default{

  props: {
      correctAnswers: Number,
      submittedQuestion: Number,
  },
  data(){
    return{
    }
  }

}

</script>

<style scoped>
p {
  /* font-size: 30px; */
}

</style>