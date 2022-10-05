<template >
  <div class="board-item">
    <h3>Estamos a : <b>{{board.actualRange}}</b></h3>
    <p class="description">
      {{ board.description }}
    </p>
    <div class="board-footer">
      <button @click="resetBoardTime()" class="btn-reset">Reiniciar</button>
      <button @click="removeBoard()" class="btn-delete">Deletar</button>
    </div>
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
.board-item {
  position: relative;
  box-sizing: border-box;
  width: 350px;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
  user-select: none;
  border: 1px solid;
  margin: 10px;
  overflow-wrap: break-word;
}

.board-footer {
  position: absolute;
  bottom: 10px;
  margin: 10px 0;
  width: 100%;
  text-align: center;
}

.btn-delete {
  background: #e85c5c;
  border: white solid;
  color: white;
  padding: 8px;
  border-radius: 0 8px 8px 0;
  ;
}

.btn-reset {
  color: black;
  background: #f8de61;
  border: white solid;
  padding: 8px;
  border-radius: 8px 0 0 8px;
}
</style>