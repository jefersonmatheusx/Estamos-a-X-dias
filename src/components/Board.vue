<template >
  <div class="boardItem">
    <h3>Estamos a : <b>{{board.actualRange}}</b></h3>
    <p class="subject">
      {{ board.description }}
    </p>

    <button @click="resetBoardTime()">Reiniciar</button>
    <button @click="removeBoard()">Deletar</button>
    <div>
      <i v-if="board.reseted">maior período foi: {{board.maxRange}}</i>
    </div>
  </div>
</template>

<script>
import * as moment from "moment";

export default {
  props: { board: { type: Object, required: true } },
  data: function () {
    return {
      mutableBoard: this.board
    }
  },
  created() {
    this.range();
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
      const arrayRange = [years + ' anos', months + ' meses', days + ' dias', hours + ' horas', minutes + ' minutos', seconds + ' segundos']
        .reduce((acc, current) => {
          if (current.split(' ')[0] > 0) {
            acc.push(current)
          }
          return acc
        }, [])
      textRange = arrayRange.toString().replace(/,/g, ',  ')

      this.mutableBoard.actualRange = textRange;
      this.mutableBoard.rangeSeconds += seconds
    },
    resetBoardTime() {
      if (this.mutableBoard.maxRangeSeconds < this.mutableBoard.rangeSeconds) {
        this.mutableBoard.maxRangeSeconds = this.mutableBoard.rangeSeconds
        this.mutableBoard.maxRange = this.mutableBoard.actualRange
      }
      this.mutableBoard.rangeSeconds = 0
      this.mutableBoard.dateStart = new Date()
      this.mutableBoard.reseted = true
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