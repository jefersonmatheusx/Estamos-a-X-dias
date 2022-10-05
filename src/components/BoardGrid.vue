<template>
  <div class="board-content">
    <h1 class="title">Estamos a <b class="logoX">X</b> dias</h1>
    <CreateBoard class="creationForm" @addBoard="this.boards.push($event)" />
    <div class="board-grid">
      <Board v-for="(b,i) in boards" :key="b.id" :board="b" @removeBoard="removeBoard(i)" />
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
      // dateStart: new Date(), description: 'teste', maxRange: '', actualRange: ''
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
};
</script>

<style>
.board-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin: 10px
}

.description {
  display: list-item;
  margin: 4px 10px 17px 20px;
  min-height: 100px;
  margin-bottom: 50px;
}

.logoX {
  text-shadow: 7px 10px 10px black;
  font-size: 100px;
  margin: 0px 10px
}

.title {
  margin-bottom: 35px;
  font-weight: 300;
  font-size: 3rem;
  text-align: center;
}
</style>
