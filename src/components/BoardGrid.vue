<template>
  <div class="board">
    <h1 class="title"> Estamos a <b>X</b> dias </h1>
    <CreateBoard class="creationForm" @addBoard="this.boards.push($event)" />
    <div class="boards">
      <div
        class="boardItem"
        v-for="(board, index) in boards"
        :key="board.description"
      >
        estamos a <b>{{ range(index) }}</b
        >:
        <p class="subject">
          {{ board.description }}
        </p>
        <button @click="board.dateStart = new Date()">Reiniciar</button>
        <button @click="removeBoard(index)">Deletar</button>
      </div>
    </div>
  </div>
</template>

<script>
import * as moment from 'moment'
import CreateBoard from '@/components/BoardCreation'
export default {
  components: {
    CreateBoard,
  },
  data: () => ({
    boards: [],
  }),
  watch: {
    boards: {
      deep: true,
      handler() {
        localStorage.setItem('myBoards', JSON.stringify(this.boards))
      },
    },
  },
  created() {
    const json = localStorage.getItem('myBoards')
    const array = JSON.parse(json)
    this.tasks = []
    if (Array.isArray(array)) {
      this.boards = array
    }
  },
  methods: {
    range(i) {
      const references = {
        minutes: 'minutos',
        hours: 'horas',
        days: 'dias',
        months: 'meses',
      }
      let duration = 0
      let range = ''
      Object.keys(references)
        .reverse()
        .map((ref) => {
          const start = moment(this.boards[i].dateStart)
          const today = moment()
          if (duration == 0) {
            duration = today.diff(start, ref)
            range = duration + ' ' + references[ref]
          }
        })
      return range
    },
    removeBoard(i) {
      this.boards.splice(i, 1)
    },
  },
}
</script>

<style>
.board {
  /* display: flex; */
  /* flex: 1;
  flex-direction: column; */
  align-items: center;
  /* height: 10vh; */
}

.boardItem {
  padding: 10px;
  border: 1px solid;
  border-radius: 12px;
  margin: 10px 0;
  overflow-wrap: break-word;
}
.boards {
  display: block;
  position: relative;
  margin-top: 8px;
  width: 90vw;
  z-index: 0;
}
.subject {
  display: list-item;
  margin: 4px 10px 17px 20px;
}
.title {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
