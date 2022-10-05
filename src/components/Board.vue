<template >
  <div class="boardItem">
    <h3>Estamos a : <b>{{board.actualRange}}</b></h3>
    <p class="subject">
      {{ board.description }}
    </p>

    <button @click="mutableBoard.dateStart = new Date()">Reiniciar</button>
    <button @click="removeBoard()">Deletar</button>
  </div>
</template>

<script>
import * as moment from "moment";

export default {
  props: ['board'],
  data: function () {
    return {
      mutableBoard: this.board
    }
  },
  created() {
    setInterval(() => {
      this.range();
    }, 1000)
  },
  methods: {
    range() {

      const start = moment(this.board.dateStart);
      const today = moment();
      let textRange = ''
      let { seconds, minutes, hours, days, months, years } = moment.duration(today.diff(start))._data
      console.log({ seconds, minutes, hours, days, months, years })

      // y + m + d
      // m + d
      // d + h

      // --- hours range
      // h + +min + seg
      // m  + seg
      // seg
      textRange = seconds + ' segundos'

      this.mutableBoard.actualRange = textRange;
    },
    removeBoard() {
      this.$emit('removeBoard')
    }
  },
}
</script>
    
<style>
.boardItem {
  padding: 10px;
  border: 1px solid;
  border-radius: 12px;
  margin: 10px 0;
  overflow-wrap: break-word;
}
</style>