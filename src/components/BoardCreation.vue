<template>
  <div>
    Estamos a X dias
    <span
      ><textarea
        rows="2"
        type="text"
        name="description"
        :placeholder="sample"
        id=""
        v-model="description"
        class="description"
      />
      <button @click="addBoard">Criar</button></span
    >
  </div>
</template>

<script>
import * as moment from 'moment'
export default {
  data: () => ({
    description: '',
    samples :[
      'sem quebrar pratos',
      'sem falar palavrão',
      'comprometidos com o trabalho',
      'sem atrasar as reuniões',
      'sem brigar com o cachorro',
      'sendo gentis com os vizinhos',
      'praticando esportes'
      ]
  }),
  computed:{
    sample(){
      return this.samples[Math.floor(Math.random()*this.samples.length )]
    }
  },
  methods: {
    addBoard() {
      const {description,$emit} = this
      const objBoard = { description, maxDays: 0, dateStart: moment()}
      $emit('addBoard', objBoard)
    },
  },
}
</script>

<style>
.description{
  min-width: 100px;
}
</style>