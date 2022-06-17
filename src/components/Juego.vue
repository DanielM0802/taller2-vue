<template>

  <div class="juego">

    <div class="juego-area">

      <div class="juego-titulo">
        <h1>Juego</h1>
      </div>

      <board :cuadrados="cuadrados" :ganador="ganador" @click="click" />

      <div class="juego-info">

        <p v-if="stepNumber === 0">
          Vamos a comenzar<b :class="jugadorActual">{{ jugadorActual }}</b>!
        </p>
        <p v-else-if="!!ganador">
          El ganador es:&nbsp;
          <b :class="jugadorActual">{{ jugadorActual }}</b>!&nbsp;
          <button @click="restart">Jugar de nuevo</button>
        </p>
        <p v-else-if="stepNumber > 8">
          Se logro!!&nbsp;
          <button @click="restart">Jugar de nuevo</button>
        </p>
        <p v-else>
          Ahora es el turno del jugador&nbsp;
          <b :class="jugadorActual">{{ jugadorActual }}</b>!&nbsp;Acto.
        </p>
        
      </div>

    </div>

  </div>

</template>

<script>
export default {
  name: 'Juego',
  components: {
    Tablero: () => import('./Tablero')
  },
  data () {
    return {
      cuadrados: Array(9).fill(null),
      stepNumber: 0,
      jugadorActual: 'X',
      ganador: null
    }
  },
  methods: {
    hasganador() {
      if (this.ganador) return true

      const cuadrados = this.cuadrados
      const matches = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7],
        [2, 5, 8], [0, 4, 8], [2, 4, 6]
      ]

      for (let i = 0; i < matches.length; i++) {
        const [a, b, c] = matches[i]
        if (cuadrados[a] && cuadrados[a] === cuadrados[b] && cuadrados[a] === cuadrados[c]) {
          this.ganador = [ a, b, c ]
          return true
        }
      }

      return false
    },

    restart() {
      this.cuadrados = Array(9).fill(null)
      this.stepNumber = 0
      this.jugadorActual = this.jugadorActual
      this.ganador = null
    },

    click (i) {
      if (this.cuadrados[i] || this.ganador) return
      this.$set(this.cuadrados, i, this.jugadorActual)
      if (!this.hasganador()) {
        this.stepNumber++
        this.jugadorActual = this.jugadorActual === 'X' ? 'O' : 'X'
      }
    }
  }
}
</script>

<style scoped>

</style>