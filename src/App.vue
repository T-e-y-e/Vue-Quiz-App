<template>
  <div id="app">
    <div v-show="homePage" class="homepage">
     <div class="container">
        <div class="left-div px-3">
           <h1 class="welcome mb-3">Quiz App</h1>
           <p>Test your knowledge on your preferred area by answering 10 random questions. 
             All you have to do is select your preferred category and start quiz</p>
           
      </div>
      <div class="gallery1">

      </div>
      <div class="gallery2">

      </div>
      <div class="form-group mb-4 px-4 d-flex flex-column align-items-center justify-content-center">
              <div>
                <label for="" class="fw-bolder"><h3>Select Category here</h3></label><br>
              <select class="select-box mt-3" name="" id="categories" @change="changeCategory()">
                <option value="0" class="fw-bold">Select Category</option>
                <option value="1">General Knowledge</option>
                <option value="2">Computer Science</option>
                <option value="3">Mathematics</option>
                <option value="4">Science and Nature</option>
                <option value="5">Animals</option>
                <option value="6">Art</option>
                <option value="7">History</option>
                <option value="8">Geography</option>
              </select>
              </div>
              <div class="mt-5">
                <button class="btn btn-start" @click="startQuiz()">Start Quiz</button>
              </div>
              
            </div>
     </div>

  </div>

    <Header 
    :numCorrect="numCorrect"
    :numTotal="numTotal"
    :heading="heading"
    v-show = "header"
    />

    <General
    v-if="generalQuests.length && showGen"
      :currentQuestion = "generalQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showGen"
    />

    <Computer
    v-if="csQuests.length && showCom"
      :currentQuestion = "csQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showCom"
    />

    <Maths
    v-if="mathQuests.length && showMaths"
      :currentQuestion = "mathQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showMaths"
    />

    <Science
    v-if="snQuests.length && showScience"
      :currentQuestion = "snQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showScience"
    />

    <Animals
    v-if="animalQuests.length && showAnimals"
      :currentQuestion = "animalQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showAnimals"
    />

    <Art
    v-if="artQuests.length && showArt"
      :currentQuestion = "artQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showArt"
    />

    <History
    v-if="historyQuests.length && showHistory"
      :currentQuestion = "historyQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showHistory"
    />

    <Geography
    v-if="geoQuests.length && showGeo"
      :currentQuestion = "geoQuests[index]"
      :next = "next"
      :increment="increment"
      v-show= "showGeo"
    />

    <div class="rating-section" v-show="numTotal === 10 && gradePage">
      <div class="rating">
        <div class="mb-4">
          <h4>Quiz Result</h4>
        </div>
        <div class="mb-3">
          <img src="./assets/medal.png" alt="" class="medal">
        </div>
        <div class="mb-4">
          <h5 class="text-warning">Congratulations!</h5>
        </div>
        <div>
           <h2 class="text-left mb-3">Final Score: <span class="text-light ms-2">{{ numCorrect}}/{{numTotal}}</span></h2>
        <h3 class="text-left">Rating: <span class="ms-2 text-light">{{ grade()}}</span> </h3>
        </div>
        
      <button class="btn btn-try mt-5 fw-bold" @click="refresh">Try Again</button>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Computer from './components/Computer.vue'
import Maths from './components/Maths.vue'
import Science from './components/Science.vue'
import General from './components/Generalsect.vue'
import Animals from './components/Animals.vue'
import Art from './components/Art.vue'
import History from './components/History.vue'
import Geography from './components/Geography.vue'
// import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Computer,
    Maths,
    Science,
    General,
    Animals,
    Art,
    History,
    Geography
  },

  data(){
        return{
         generalQuests: [],
         csQuests: [],
         mathQuests: [],
         snQuests: [],
         animalQuests: [],
         artQuests: [],
         historyQuests: [],
         geoQuests: [],
         index: 0,
         heading: "",
         numCorrect: 0,
         numTotal: 0,
         rating: "",
         selectedCat: 0,
         homePage: true,
         gradePage: true,
         header: false,
         showGen: false,
         showCom: false,
         showMaths: false,
         showScience: false,
         showAnimals: false,
         showArt: false,
         showHistory: false,
         showGeo: false,
        }
    },

   methods: {
        next(){
           this.index++
        },

        increment(isCorrect){
          if(isCorrect){
            this.numCorrect++
          }
          this.numTotal++
        },

        general(){
            axios.get("https://opentdb.com/api.php?amount=10&category=9&type=multiple")
            .then((response) => {
                this.generalQuests = response.data.results
            })
        },
         computerScience(){
            axios.get("https://opentdb.com/api.php?amount=10&category=18&type=multiple")
            .then((response) => {
                this.csQuests = response.data.results
            })
        },
         mathematics(){
            axios.get("https://opentdb.com/api.php?amount=10&category=19&type=multiple")
            .then((response) => {
                this.mathQuests = response.data.results
            })
        },
         scienceNature(){
            axios.get("https://opentdb.com/api.php?amount=10&category=17&type=multiple")
            .then((response) => {
                this.snQuests = response.data.results
            })
        },
         animals(){
            axios.get("https://opentdb.com/api.php?amount=10&category=27&type=multiple")
            .then((response) => {
                this.animalQuests = response.data.results
            })
        },
         art(){
            axios.get("https://opentdb.com/api.php?amount=10&category=25&type=multiple")
            .then((response) => {
                this.artQuests = response.data.results
            })
        },
         history(){
            axios.get("https://opentdb.com/api.php?amount=10&category=23&type=multiple")
            .then((response) => {
                this.historyQuests = response.data.results
            })
        },
         geography(){
            axios.get("https://opentdb.com/api.php?amount=10&category=22&type=multiple")
            .then((response) => {
                this.geoQuests = response.data.results
            })
        },

           changeCategory(){
           let categories =  document.getElementById("categories");
           let selectedCategory = categories.options[categories.selectedIndex].value;

           
           switch(selectedCategory){

                  case "1":
                   this.selectedCat = 1;
                   this.heading = "General Knowledge"
                   break;

                   case "2":
                   this.selectedCat = 2;
                   this.heading = "Computer Science"
                   break;

                   case "3":
                   this.selectedCat = 3;
                   this.heading = "Mathematics"
                   break;

                   case "4":
                   this.selectedCat = 4;
                   this.heading = "Science and Nature"
                   break;

                   case "5":
                   this.selectedCat = 5;
                   this.heading = "Animals"
                   break;

                   case "6":
                   this.selectedCat = 6;
                   this.heading = "Art"
                   break;

                   case "7":
                   this.selectedCat = 7;
                   this.heading = "History"
                   break;

                   case "8":
                   this.selectedCat = 8;
                   this.heading = "Geography"
                   break;

                   default:
                     this.selectedCat = 0;
                     break;
           }
       },

       startQuiz(){
         if(this.selectedCat === 1){
                   this.showGen = true;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 2){
             this.showGen = false;
                   this.showCom = true;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 3){
           this.showGen = false;
                   this.showCom = false;
                   this.showMaths = true;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 4){
              this.showGen = false;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = true;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 5){
             this.showGen = false;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = true;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 6){
            this.showGen = false;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = true;
                   this.showHistory = false;
                   this.showGeo = false;
                   this.header = true;
         }
         else if(this.selectedCat === 7){
            this.showGen = false;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = true;
                   this.showGeo = false;
                   this.header = true;
                   this.homePage = false
         }
         else if(this.selectedCat === 8){
           this.showGen = false;
                   this.showCom = false;
                   this.showMaths = false;
                   this.showScience = false;
                   this.showAnimals = false;
                   this.showArt = false;
                   this.showHistory = false;
                   this.showGeo = true;
                   this.header = true;
                   this.homePage = false
         }
         else{
           alert("Select a category")
           this.homePage = true
         }
         this.numTotal = 0;
        this.numCorrect = 0;
        this.index = 0
       },

       refresh(){
         this.homePage = true;
         this.gradePage = true;
         this.showCom = false;
         this.showGen = false;
         this.showMaths = false;
         this.showScience = false;
         this.showAnimals = false;
         this.showArt = false;
         this.showHistory = false;
         this.showGeo = false;
         this.header = false;
         this.numTotal = 0;
         this.numCorrect = 0;
         this.index = 0
       },

       grade(){
         if (this.numCorrect <= 5){
           return " Fair"
         }
         else if(this.numCorrect > 5 && this.numCorrect < 8){
           return "Good"
         }
         else if(this.numCorrect > 8){
           return "Very Good"
         }
       }
    },
    mounted(){
      this.general();
      this.computerScience();
      this.mathematics();
      this.scienceNature();
      this.animals();
      this.art();
      this.history();
      this.geography()
    }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}

.nav{
  background-color: #E6E8F5;
  color: rgb(24, 23, 23);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80px;
}

.nav h1{
   font-size: 50px;
}

.homepage{
  background-color: rgb(16, 16, 59);
  height: 100vh;
  width: 100vw;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
}

.select-box{
  background-color: rgb(204, 197, 197);
  width: 240px;
  height: 40px;
  padding: 0.6rem 0.8rem;
  border-radius: 5px;
  border: none;
  font-weight: bold;
}

.select-box option{
  background-color: white;
  font-weight: bold;
  color: rgb(56, 55, 55);
  border-radius: 5px;
  padding: 0.6rem;
  padding-bottom: 1rem;
}

.btn-start{
  background-color: #FFC352;
  color: rgba(0, 0, 0, 0.9);
  text-transform: uppercase;
  font-weight: bold;
  padding: .8rem 1.5rem;
}

.welcome{
  color: #FFC352;
}

.container{
  background-color: rgb(40, 40, 77);
  color: white;
  box-shadow: 0px 0px 52px -28px rgba(0,0,0,1);
  height: 80%;
  width: 70vw;
   display: grid;
  grid-template-columns: 50% 50%;
  grid-template-rows: 50% 50%;
  margin-top: 20px;
  padding: 0;
  border-radius: 10px;
  overflow: hidden;
  font-size: 17px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.gallery1{
   background: url("./assets/girl.jpg") no-repeat center center/cover;
}

.gallery2{
  background: url("./assets/lady.jpg") no-repeat center center/cover;
}

.left-div{
  width: 100%;
  color: white;
  padding-top: 50px;
}

.rating-section{
  background-color: rgb(16, 16, 59);;
  height: 100vh;
  width: 100vw;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.rating{
  width: 320px;
  height: 480px;
  border-radius: 10px;
  color: white;
  text-align: left;
  background-color: rgb(40, 40, 77);
  box-shadow: 0px 0px 52px -28px rgba(0, 0, 0, 0.6);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 17px;
}

.rating h2, .rating h3{
  color: rgb(230, 230, 7);
}

.medal{
  width:100px;
}

.btn-try{
  background-color: #FFC352;
  color: rgba(0, 0, 0, 0.9);
  text-transform: uppercase;
  font-weight: bold;
  font-size: 18px;
  padding: .8rem 1.5rem;
}

@media screen and (max-width: 992px) {
  .container{
    background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)),
  url("./assets/girl.jpg") no-repeat center center/cover;
    width: 95vw;
    grid-template-columns: auto;
    grid-template-rows: 40% 60%;
    height: 95vh;
    font-size: 20px;
  }

  .gallery1{
    display: none;
  }

  .gallery2{
    display: none;
  }

  .select-box{
    width: 80vw;
    height: 50px;
  }
}
</style>
