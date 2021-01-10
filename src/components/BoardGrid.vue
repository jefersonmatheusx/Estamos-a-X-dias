<template>
  <div class="boards">
    <CreateBoard @addBoard="this.boards.push($event)"/>
    <div class='boardItem' v-for="(board, index) in boards" :key="board.description">
      estamos a {{ range(index) }} {{ board.description }} <button @click="board.dateStart=new Date()">Reiniciar</button>
    </div>
  </div>
</template>

<script>
import * as moment from 'moment'
import CreateBoard from '@/components/BoardCreation'
export default {
  components:{
    CreateBoard
  },
  data:()=>({
     boards: [],
  }),
  methods: {
  range(i) {
      const references = { minutes: 'minutos', hours: 'horas', days: 'dias', months:'meses' }
      let duration = 0
      let range = ''
      Object.keys(references)
        .reverse()
        .map((ref) => {
          const start = moment(this.boards[i].dateStart)
          const today = moment()
          if (duration == 0) {
            duration = today.diff(start,ref)
            range = duration + ' ' + references[ref]
          }
        })
      return range
    },
  },
}
</script>

<style>
.boardItem{
      padding: 10px;
    border: 1px solid;
    border-radius: 12px;
    margin: 10px 0;
    overflow-wrap: break-word;
}
</style>
