<template>
<div>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying" >Play</button> 
  <!-- Disabled é uma propriedade nativa do html que quando adicionamos um bind usamos ele dinamicamente para desabilitar o botão enquanto o jogo está rodando -->
  <Block v-if="isPlaying" :delay="delay" @end="endGame"/>
  <Results v-if="showResult" :score="score"/>
</div>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'


export default {
  components: { Block, Results },
  coomponents: {
    Block,
    Results
  },
  data(){
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResult: false
    }
  },
  methods: {
    start(){
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      console.log(this.delay)
      this.showResult = false
    },
    endGame(reactionTime){
      //o parametro reactionTime é o valor que recebemos do $emit do componente filho nesse caso.
      this.score = reactionTime
      this.isPlaying = false
      this.showResult = true
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
</style>
