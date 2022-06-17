<template>

    <div class="tablero" v-if="cuadrados">

        <div v-for="fila in 3" :key="fila" class="tablero-fila">

            <cuadrado v-for="i in 3" :key="indexPorFila(i, fila)" :value="cuadrados[indexPorFila(i, fila)]" 
                :disabled="!!ganador" :ganador="!!ganador && ganador.includes(indexPorFila(i, fila))" @click="click(i, fila)" />

        </div>

  </div>

</template>

<script>

export default {
  name: 'Tablero',
  props: {
    cuadrados: Array,
    ganador: Array
  },
  components: {
    Cuadrado: () => import('./Cuadrado')
  },
  methods: {
    indexPorFila (index, fila, max = 3) {
      return (fila * max + index) - (max + 1)
    },

    click (index, fila) {
      this.$emit('click', this.indexPorFila(index, fila));
    }
  }
}

</script>

<style scoped>
</style>
