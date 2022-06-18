<template>
  <div class="game">
    <div class="game-area">
      <div class="game-title">
        <h1>Juego del Gato</h1>
      </div>

      <Tablero :squares="squares" :winner="winner" @click="click" />

      <div class="game-info">
        <p v-if="stepNumber === 0" class="msg">
          Es turno del jugador: &nbsp;<b :class="currentPlayer">{{  currentPlayer }}</b>!
        </p>
        <p v-else-if="!!winner" class="msg">
          El ganador es: &nbsp;<b :class="currentPlayer"> {{ currentPlayer }}</b>!&nbsp;
          <button @click="restart">Jugar de nuevo</button>
        </p>
        <p v-else-if="stepNumber > 8" class="msg">
          ¡Empate!
          <button @click="restart">Jugar de nuevo</button>
        </p>
        <p v-else class="msg">
          Es turno del jugador: &nbsp;<b :class="currentPlayer">{{ currentPlayer }}</b>
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
      squares: Array(9).fill(null),
      stepNumber: 0,
      currentPlayer: 'X',
      winner: null
    }
  },
  methods: {
    hasWinner() {
      if (this.winner) return true

      const squares = this.squares
      const matches = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7],
        [2, 5, 8], [0, 4, 8], [2, 4, 6]
      ]

      for (let i = 0; i < matches.length; i++) {
        const [a, b, c] = matches[i]
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          this.winner = [ a, b, c ]
          return true
        }
      }

      return false
    },

    restart() {
      this.squares = Array(9).fill(null)
      this.stepNumber = 0
      this.currentPlayer = this.currentPlayer
      this.winner = null
    },

    click (i) {
      if (this.squares[i] || this.winner) return
      this.$set(this.squares, i, this.currentPlayer)
      if (!this.hasWinner()) {
        this.stepNumber++
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X'
      }
    }
  }
}
</script>

<style scoped>
.game {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-area {
  display: flex;
  flex-flow: column;
}

.game-title {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 0 3vmin;
}

.game-title img {
  margin: 0 12px 0 -20px;
  width: 40px;
}

.game-title h1 {
  margin: 0;
  font-size: 2.25em;
  color: blue;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.game-info {
  margin: 3vmin 0 0;
  padding: 1rem .5rem;
  font-size: 1.25em;
  text-align: center;
  background: #fff6;
  color: #111;
}

.game-info p {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-info .X {
  color: red;
}

.game-info .O {
  color: blue;
}

.game-info button {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-weight: 500;
  font-size: 18px;
  border-width: 0px;
  border-radius: 13px;
  height: 40px;
  width: 170px;
  margin-left: 40px;
  background-color: cadetblue;
  color: white;
  cursor: pointer;
  outline: none;
}

.msg {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

</style>