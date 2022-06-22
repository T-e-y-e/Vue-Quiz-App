<template>
  <div class="d-flex justify-content-center main pt-5">
  <div class="card" style="width: 40rem;">
  <div class="card-body mb-5">
    <p class="card-text">{{ currentQuestion.question }}</p>
  </div>
  <ul class="list-group list-group-flush">
    <li class="list-group-item mb-3" v-for="(answer, index) in shuffledAnswers" :key="index" @click="selectAnswer(index)"
    :class="answerClass(index)">{{ answer }}</li>
  </ul>
  <div class="card-body d-flex justify-content-evenly">
    <button type="button" class="btn btn-primary" @click="submitAnswer" :disabled="selectedIndex === null || answered" v-show="!answered">SUBMIT</button>
    <button type="button" class="btn btn-next" v-show="answered" @click="next">NEXT</button>
  </div>
</div>
  </div>
</template>

<script>
import _ from "lodash"

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },

  data(){
        return{
          selectedIndex: null,
          correctIndex: null,
          shuffledAnswers: [],
          answered: false
        }
    },

    methods: {
       selectAnswer(index){
         this.selectedIndex = index
       },

       submitAnswer(){
          let isCorrect = false

          if(this.selectedIndex === this.correctIndex){
            isCorrect = true
          }
          this.answered = true
          this.increment(isCorrect)
       },

       answerClass(index){
          let answerClass = ''

          if(!this.answered && this.selectedIndex === index){
            answerClass = 'selected'
          }
          else if(this.answered && this.correctIndex === index){
            answerClass = 'correct'
          }
          else if(this.answered && this.selectedIndex === index && this.correctIndex !== index){
            answerClass = 'incorrect'
          }

          return answerClass
       },

       shuffleAnswers(){
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
        this.shuffledAnswers = _.shuffle(answers);
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
       }
    },

    watch:{
      currentQuestion: {
        immediate: true,
        handler(){
        this.selectedIndex = null;
        this.answered = false
        this.shuffleAnswers()
        }
      }
    },

  // computed: {
  //   answers(){
  //     // let answers = [...this.currentQuestion.incorrect_answers];
  //     // answers.push(this.currentQuestion.correct_answer);
  //     // return answers
  //     let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
  //     answers = _.shuffle(answers)
  //     return answers
  //   }
  // },

}
</script>

<style scoped>
.main{
  background-color: rgb(234, 234, 243);
  height: 80vh;
}
.card{
  background-color: transparent;
  border: none;
  height: max-content;
}

.list-group-item{
  background-color: rgb(203, 203, 214);
  border-radius: 8px;
  border: none;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
}

  .card-text{
    color: black;
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-size: 18px;
    
  }

  .card-text::after{
    content: "";
    width: 150px;
    height: 3px;
    background-color: #FFC352;
    margin-top: 10px;
  }

  .btn{
    color: white;
    font-weight: bold;
    padding: 0.65rem 0.9rem;
  }

  .btn-next{
    background-color: #df5c23;
  }

  .selected{
    background-color: rgb(65, 65, 163);
    color: white;
  }

  .correct{
    background-color: green;
    color: white;
  }

  .incorrect{
    background-color: red;
    color: white
  } 

  @media screen and (max-width: 992px) {
    .list-group-flush{
       display: flex;
       justify-content: center;
       align-items: center;
    }

    .list-group-item{
      width: 95vw;
    }
  }
</style>
