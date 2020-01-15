<template>
  <div id="app">
    <!-- <HelloWorld msg=""/> -->
    <Guess></Guess>
    <!-- <Follow></Follow> -->
    <Board></Board>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Guess from './components/Guess.vue'
//import Follow from './components/Follow.vue'
import Board from './components/Board.vue'

export default {
  name: 'app',
  components: {
    // HelloWorld,
    Guess,
    //Follow,
    Board
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
  margin: 0;
}
</style>
