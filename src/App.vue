<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
          <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <component :is="activeCmpt" @answered="switchCmpt($event)" @confirmed="activeCmpt = 'app-question-cmpt'"> 
            </component>
          </div>
        </div>
    </div>
</template>

<script>
import CorrectComponent from './components/CorrectComponent.vue';
import WrongComponent from './components/WrongComponent.vue';
import QuestionComponent from './components/QuestionComponent.vue';
  export default {
    data () {
      return {
        activeCmpt: 'app-question-cmpt'
      }
    },
    methods: {
      switchCmpt(isCorrect){
        // let counter = 0;
        // console.log(isCorrect)
        // if(counter === 0){
        //   this.activeCmpt = 'app-question-cmpt'
        //   counter++;
        // }
        if(isCorrect){
          this.activeCmpt = 'app-correct-cmpt'
        }else{
          this.activeCmpt = 'app-wrong-cmpt'
        }
      }
    },
    components:{
      'app-correct-cmpt': CorrectComponent,
      'app-wrong-cmpt': WrongComponent,
      'app-question-cmpt': QuestionComponent,
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
