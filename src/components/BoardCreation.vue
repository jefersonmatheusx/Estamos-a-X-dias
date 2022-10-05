<template>
  <div class="new-board">
    <span class="new-board-form">
      <textarea rows="2" type="text" name="description" :placeholder="sample" id="" v-model="description"
        class="description form-element" />
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
      const objBoard = { description, maxDays: 0, dateStart: moment() };
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
  display: flex;
  text-align: center;
  /* width: 86vw; */
  flex-direction: column;
  align-items: center;
}

.form-element {
  outline: none;
  font-size: 16px;
  border: 1px solid #fff;
  padding: 5px 10px 8px;

  box-sizing: border-box;
}

textarea.form-element {
  width: 100% !important;
  background: #ddf8ff;
  border-radius: 8px 8px 0 0;
  min-height: 88px;
}

button.form-element {
  border-top: none;
  background: #2196f3;
  border-radius: 0 0 8px 8px;
  width: 100%;
  color: #fff;
}

hr.separator {
  border-top: 1px solid white;
  border-bottom: none;
  margin-top: 23px;
}
</style>