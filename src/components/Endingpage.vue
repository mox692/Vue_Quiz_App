<template>
    <div class="title-wrapper">
        <img alt="Vue logo" src="../assets/logo.png">
        <h1>Good Job!</h1>
         <p>Here is your score!!!</p>
         <p><span class="score">{{ this.correctAnswers }}</span>poins!!</p>
    </div>
</template>

<script>
export default{
    props:{
        correctAnswers: Number
    }
}
</script>

<style scoped>
.title-wrapper{
    padding-bottom: 100px;
    /* background-color: red; */
}
.score{
    font-size: 5rem;
    font-weight: bold;
    color: lightgreen;
}
</style>