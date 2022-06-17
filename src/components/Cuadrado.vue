<template>
  <button class="cuadrado" :class="[ value, { 'winner': winner } ]"
    :disabled="disabled" @click="click">{{value}}</button>
</template>

<script>
export default {
  name: 'Cuadrado',
  props: {
    value: String,
    
    winner: Boolean,
    disabled: Boolean
  },
  methods: {
    click () {
      this.$emit('click')
    }
  }
}
</script>

<style scoped>
.cuadrado {
  font-size: 32px;
}


.cuadrado.X {
  color: red;
}

.cuadrado.O {
  color: blue;
}
</style>
