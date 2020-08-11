<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <!-- Transition na ceo red koji drzi nase komponente da bi se dobila animacija na ucitavanju
              koristimo cetiri klase koje ispisuju stanje fade-nesto klase u <style> -->
        <transition name="fade" appear mode="out-in">
          <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
              <!-- Koristimo animaciju sa neta mozemo dodati name="" pa animaciju dodati kao dole ili iskoristiti klase
                    kao u projektu vuejs-animations (pogledaj) -->
              <transition
                name="flip"
                mode="out-in">
                <component :is="activeCmpt" @answered="switchCmpt($event)" @confirmed="activeCmpt = 'app-question-cmpt'"> 
                </component>
              </transition>
            </div>
          </div>
        </transition>
    </div>
</template>

<script>
import CorrectComponent from './components/CorrectComponent.vue';
import WrongComponent from './components/WrongComponent.vue';
import QuestionComponent from './components/QuestionComponent.vue';
  export default {
    data () {
      return {
        activeCmpt: null
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
    },
    created(){
      this.activeCmpt = 'app-question-cmpt';
    }
}
</script>

<style>
.fade-enter {
    opacity: 0;
  }
.fade-enter-active {
  transition: opacity 1s;
}
.fade-leave {
  /* opacity: 1; */
}
.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}


/**flip animation prilikom load-ovanja */

.flip-enter {
  /* opacity: 0; */
}
.flip-enter-active {
  /* animation: flip-in .3s ease-out forwards; */
  animation: flipInX;
  animation-duration: .5s;
}
.flip-leave {

}
.flip-leave-active{
  animation: flipOutX;
  animation-duration: .5s;
}

@keyframes flip-out {
  from {
    transform: rotateX(0deg);
  }
  to {
    transform: rotateX(90deg);
  }
}
@keyframes flip-in {
  from {
    transform: rotateX(90deg);
  }
  to {
    transform: rotateX(0deg);
  }
}

.animate__animated.animate__flipInX {
  --animate-duration: .5s;
}
</style>
