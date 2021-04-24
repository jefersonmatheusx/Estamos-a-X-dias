<template>
<div>
    <BoardGrid />
</div>
</template>

<script>
import BoardGrid from './components/BoardGrid'

export default {
  name: 'App',
  components: {
    BoardGrid
  },
}
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
  height: 100%;
}

</style>