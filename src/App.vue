<template>
  <Juego />
</template>

<script>
export default {
  name: 'App',
  components: {
    Juego: () => import('./components/Juego')
  }
}
</script>

<style>


</style>
