<template>
<div>
  <img alt="Vue logo" src="./assets/logo.png">
  <BoardGrid :boards="boards"/>
</div>
</template>

<script>
import BoardGrid from './components/BoardGrid'

export default {
  name: 'App',
  components: {
    BoardGrid
  },
  data:()=>({
    boards:[
      {name:'Quebrar copos', type:'sem',maxDays:10, dateStart:new Date()},
      {name:'Quebrar pratos', type:'sem',maxDays:10, dateStart:'01/05/2021'},
      {name:'Vivendo', type:'',maxDays:10, dateStart:'03/21/1993'}
      ]
  })
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
