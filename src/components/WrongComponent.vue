<template>
    <div class="alert alert-danger">
      <h3>Your answer is {{correctInfo}}!</h3>
      <hr>
      <h3>{{answer}}</h3>
      <button class="btn btn-danger">Confirm</button>
    </div>
</template>

<script>
  export default {
    props:{
      answer: null
    },
    data(){
      return {
        correctInfo: 'Wrong',
      }
    }
  }
</script>

<style scoped>
  .alert-danger{
    text-align: center;
  }
  hr {
    width: 50%;
    margin: 0 auto 20px auto;
    display: block;
  }
  h3:nth-child(2) {
    color: black;
  }
</style>