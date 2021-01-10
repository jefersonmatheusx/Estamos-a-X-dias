<template>
  <div class="boards">
    <div v-for="(board, index) in boards" :key="board.name">
      estamos a {{ range(index) }} {{ board.type }} {{ board.name }}
    </div>
  </div>
</template>

<script>
import * as moment from 'moment'
export default {
  props: {
    boards: {
      type: Array,
      default: () => [
        {
          name: 'Quebrar copos',
          type: 'sem',
          maxRange: 10,
          dateStart: new Date(),
        },
      ],
      required: true,
    },
  },
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
            console.log(start.toString())
          }
        })
      return range
    },
  },
}
</script>

<style></style>
