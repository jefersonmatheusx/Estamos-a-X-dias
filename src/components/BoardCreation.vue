<template>
  <div class="new-board">
    <span class="new-board-form">
      <input rows="2" type="text" name="description" :placeholder="sample" id="" v-model="description"
        class="description-input form-element" />
      <button @click="addBoard" class="form-element">Criar</button>
    </span>
    <hr class="separator" />
  </div>
</template>

<script>
import * as moment from "moment";
export default {
  data: () => ({
    description: "",
    samples: [
      "sem quebrar pratos",
      "sem falar palavrão",
      "comprometidos com o trabalho",
      "sem atrasar as reuniões",
      "sem brigar com o cachorro",
      "sendo gentis com os vizinhos",
      "praticando esportes",
    ],
  }),
  computed: {
    sample() {
      return this.samples[Math.floor(Math.random() * this.samples.length)];
    },
  },
  methods: {
    addBoard() {
      const { description, $emit } = this;
      const objBoard = { description, maxRange: '', dateStart: moment(), actualRange: 0, reseted: false, rangeSeconds: 0, maxRangeSeconds: 0 };
      $emit("addBoard", objBoard);
      this.description = ""
    },
  },
};
</script>

<style>
.new-board {
  position: sticky;
  top: 5px;
  z-index: 1;
}

.new-board-form {
  /* display: flex; */
  /* text-align: center; */
  /* width: 86vw; */
  /* flex-direction: column; */
  /* align-items: center; */
}

.form-element {
  outline: none;
  font-size: 16px;
  border: 1px solid #fff;
  padding: 5px 10px 8px;

  box-sizing: border-box;
}

input.form-element {
  width: 70%;
  background: #ddf8ff;
  border-radius: 10px 0px 0px 10px !important;
  min-height: 88px;
}

button.form-element {
  border-left: none;
  background: #2196f3;
  border-radius: 0px 10px 10px 0px;
  width: 30%;
  color: #fff;
  height: 86px;
}

hr.separator {
  border-top: 1px solid white;
  border-bottom: none;
  margin-top: 23px;
}
</style>