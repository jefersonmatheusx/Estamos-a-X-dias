<template>
  <div class="board">
    <h1 class="title">Estamos a <b>X</b> dias</h1>
    <CreateBoard class="creationForm" @addBoard="this.boards.push($event)" />
    <div class="boards">
      <div v-for="(b,i) in boards" :key="b.id">
        <Board :board="b" @removeBoard="removeBoard(i)" />
      </div>
    </div>
  </div>
</template>

<script>
import CreateBoard from "@/components/BoardCreation";
import Board from '@/components/Board'
export default {
  components: {
    CreateBoard,
    Board
  },
  data: () => ({
    boards: [{
      dateStart: new Date(), description: 'teste', maxDays: '', actualRange: ''
    }],
  }),
  watch: {
    boards: {
      handler() {
        localStorage.setItem("myBoards", JSON.stringify(this.boards));
      },
      deep: true,
    },
  },
  created() {
    const json = localStorage.getItem("myBoards");
    const array = JSON.parse(json);
    this.tasks = [];
    if (Array.isArray(array)) {
      this.boards = array;
    }
  },
  methods: {

    removeBoard(i) {
      this.boards.splice(i, 1);
    },
  },
  // watch: {
  //   timerCount: {
  //     handler(value) {
  //       if (value > 0) {
  //         setTimeout(() => {
  //           this.timerCount--;
  //         }, 1000);
  //       }
  //     },
  //     immediate: true, // This ensures the watcher is triggered upon creation
  //   },
  // }
};
</script>

<style>
.board {
  /* display: flex; */
  /* flex: 1;
  flex-direction: column; */
  align-items: center;
  /* height: 10vh; */
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
