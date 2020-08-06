<template>
  <div class="panel panel-default">
    <div class="panel-heading text-center">
      <h3 >{{question}}</h3>
    </div>
    <div class="panel-body">
      <div 
        class="col-xs-12 col-sm-6 text-center" 
        v-for="ans in answersData" 
        :key="ans.answer">
        <button 
          class="btn btn-primary btn-lg" 
          style="margin: 10px" 
          @click="onAnswer(ans.correct)">{{ans.answer}}</button>
      </div>
    </div>
  </div>
</template>

<script>
  const ADD_MODE = 1;
  const SUB_MODE = 2;
  export default {
    data(){
      return{
        question: 'Oops, an error ocurred :/',
        answersData: [
          {correct: null, answer: 0},
          {correct: null, answer: 0},
          {correct: null, answer: 0},
          {correct: null, answer: 0},
        ]
      }
    },
    methods:{
      generateQuestion(){
        const firstNumber = this.generateRandomNumber(1,100);
        const secondNumber = this.generateRandomNumber(1,100);
        const modeNumber = this.generateRandomNumber(1,2);

        let correctAnswer


        /*Generisanje pitanja i na osnovu random broja izmedju 1 i 2 daje oduzimanje ili sabiranje */
        switch(modeNumber){
          case ADD_MODE: {
            console.log('ADD');
            this.question = 'What is ' + firstNumber + ' + ' + secondNumber + '?' ;
            correctAnswer = firstNumber + secondNumber;
            break;
          }
          case SUB_MODE: {
            console.log('SUBS')
            this.question = 'What is ' + firstNumber + ' - ' + secondNumber + '?' ;
            correctAnswer = firstNumber - secondNumber;
            break;
          }
          default: {
            this.question = 'Oops, an error ocurred :/';  
            break;
          }
        }

        /**Generisanje odgovora kroz random brojeve */
        for(let i = 0; i < 4; i++){ //imamo 4 odgovora, zato loop na 4
          this.answersData[i].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
          this.answersData[i].correct = false;
        }

        //gazimo jedan od odgovora sa tacnim odgovorom
        const correctBtn = this.generateRandomNumber(0,3);
        this.answersData[correctBtn].answer = correctAnswer;
        this.answersData[correctBtn].correct = true;

      },
      generateRandomNumber(min,max,correctAnswer){
        let rndNumber;
        rndNumber = Math.round(Math.random() * (max-min)) + min;
        if(rndNumber == correctAnswer){
          return  Math.round(Math.random() * (max-min)) + min;
        }
        console.log(rndNumber)
        return rndNumber;
      },
      onAnswer(isCorrect){
        this.$emit('answered', isCorrect)
      }
    },
    created(){
      this.generateQuestion();
    }
  }
</script>

<style scoped>
  .panel-heading{
    padding: 8px 10px
  }
  h3{
    margin-top: 10px;
  }
</style>