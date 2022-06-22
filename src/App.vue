<template>
  <h1>Ninja reaction timer {{count}}</h1>
  <div v-if="easyMode" class="noob">There is no easy mode you can play minecraft if you want !!!</div>
  <button @click="easy" :disabled="isPlaying">Easy</button>
  <button @click="medium" :disabled="isPlaying">Medium</button>
  <button @click="hard" :difficulty="difficulty" :disabled="isPlaying">Hard</button>
  <Block v-if="isPlaying" @click="increment" :delay="delay" @end="endGame"/>
  <Results v-if="showResults" :count="count"/>
</template>

<script>
var audio = new Audio('/voice.mp3')
import Block from './components/Block.vue';
import Results from "./components/Results.vue";
export default {
  name: 'App',
  components: {
    Results,
    Block
  },
  data(){
    return{
     isPlaying:false,
     delay:null,
      score:0,
      showResults:false,
      easyMode:false,
      count:0,
      difficulty:false
    }
  },
  methods:{
    easy(){
      this.easyMode = true
    },
    medium(){
      this.easyMode = false
      this.delay = 100 + Math.random() * 1500
      this.isPlaying = true
      this.showResults = false
      this.count = 0
      this.score = 0
    },
    hard(){
      this.difficulty = true
      this.easyMode = false
      this.delay = 0
      this.isPlaying = true
      this.showResults = false
      this.count = 0
      this.score = 0
    },
    increment(){
      this.count += 1
      audio.play()
    },
    endGame(count){
      this.score = count
      this.isPlaying = false
      this.showResults = true
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
  color: #2c3e50;
  margin-top: 60px;
}
button{
  background: #0faf87;
  color: #f2f2f2;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled]{
  opacity: 0.2;
  cursor: not-allowed;
  pointer-events: none;
}
.noob {
  color: red;
  font-size: 2rem;
}
</style>
