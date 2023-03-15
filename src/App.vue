<template>
  <h1>Hawk Eye</h1>
  <div class="welcome" v-if="showWelcomeTarget">
    <p >Test your reflexes!</p>
    <p>You will be ranked by your reaction time and accuracy.</p>
    <p>Rules: Click as fast and as precise as you can on the target below.</p>
    <p>Click "Play" to start!</p>
  </div>
  <button @click="startGame" :disabled="isPlaying">Play</button>
  
  <Results v-if="showResults" :score="score" :scorePrecision="scorePrecision" :finalResult="finalResult"/>
<div class="container" @end="endGame">
  <Target v-if="isPlaying" :delay="delay" @end="endGame"/>
  <img v-if="showWelcomeTarget" class="target-welcome" src="./assets/images/target.png" alt="" >
</div>

</template>

<script>
import Target from './components/Target.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Target, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      scoreTime: null,
      showResults: false,
      scorePrecision: null,
      finalResult: 0,
      showWelcomeTarget: true
    }
  },
  methods: {
   startGame() {
     this.delay = 1000 + Math.random() * 2000,
     this.isPlaying = true
     this.showResults = false
     this.showWelcomeTarget = false
   },
   endGame(resultsObj) {
      this.scoreTime = resultsObj.ReactTime
      this.isPlaying = false
      this.showResults = true
      this.scorePrecision = resultsObj.Target
      this.finalResult = Math.round((1/this.scoreTime) * this.scorePrecision * 90)


      // console.log("scorePrecision " + this.scorePrecision)
   }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(29, 59, 99);
  margin-top: 20px;
}
.welcome {
  width: 90%;
  margin: auto;
  height: 180px;
}
.welcome p {
  margin: 10px;
  font-size: 18px;
}
button {
  width: 100px;
  height: 50px;
  margin-bottom: 1rem;
  border-radius: 10px;
  background: rgb(29, 59, 99);
  color: white;
  font-size: 22px;
  cursor: pointer;
}
button:disabled {
  background: rgb(133, 133, 133, 0.8);
  color: rgb(207, 207, 207);
  opacity: .8;
}
.target-welcome {
  margin: 10px;
  width: 30%;
}
html {
  background-color: #f0ac7c34;
  background-image: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 42 44' xmlns='http://www.w3.org/2000/svg'%3E%3Cg id='Page-1' fill='none' fill-rule='evenodd'%3E%3Cg id='brick-wall' fill='%23770700' fill-opacity='0.09'%3E%3Cpath d='M0 0h42v44H0V0zm1 1h40v20H1V1zM0 23h20v20H0V23zm22 0h20v20H22V23z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

@media screen and (max-width: 800px) {
  .target-welcome {
    margin: 10px;
    width: 50%;
  }
}

@media screen and (max-width: 600px) {
  .welcome {
    height: 200px;
  }
  .target-welcome {
    margin: 10px;
    width: 60%;
  }
}
</style>
