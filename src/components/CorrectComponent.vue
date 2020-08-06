<template>
    <div class="alert alert-success">
      <h3>Your answer is {{correctInfo}}!</h3>
      <hr>
      <h3>{{answer}}</h3>
      <button class="btn btn-success" @click="confirm">Confirm</button>
    </div>
</template>

<script>
  export default {
    props:{
      answer: null
    },
    data(){
      return {
        correctInfo: 'Correct',
      }
    },
    methods:{
      confirm(){
        this.$emit('comfirmed');
      }
    }
  }
</script>

<style scoped>
  .alert-success{
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