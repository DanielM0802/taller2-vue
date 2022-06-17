<template>
  <div id="app">
    <Juego />
  </div>
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
