<template>
  <div id="app">

  
    <!-- <HelloWorld msg=""/> -->
    <Code></Code>
    
    <!-- <Follow></Follow> -->
    <!-- <Board></Board> -->
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

import Code from './components/Decode.vue'
//import Follow from './components/Follow.vue'
//import Board from './components/Board.vue'


export default {
  name: 'app',
  components: {
    // HelloWorld,
    Code,

    // Follow,
    // Board,
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
