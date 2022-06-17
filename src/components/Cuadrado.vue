<template>
    <button class="cuadrado" :class="[ contenido, { 'ganador': ganador } ]"
    :disabled="desactivado" @click="onClick">{{contenido}}</button>
</template>

<script>
export default {
  props: {
    contenido: String,
    ganador: Boolean,
    desactivado: Boolean
  },
  methods: {
    onClick () {
      this.$emit('click')
    }
  }
}
</script>

<style>
.cuadrado {
  background: red;
 
}


</style>