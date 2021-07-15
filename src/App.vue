<template>
  <div id="app">
    <span><strong>Tic Tac Toe</strong></span> <small>in VueJS</small>
    <Board v-if="players.length > 1" :players="players" />
    <LoginPlayers v-else @setNewPlayers="setNewPlayers" />
  </div>
</template>

<script>
import Board from './components/Board.vue';
import LoginPlayers from './components/LoginPlayers.vue';

export default {
  name: 'App',
  components: {
    Board,
    LoginPlayers
  },
  data() {
    return {
      players: []
    }
  },
  methods: {
    setNewPlayers(players) {
      this.players = players
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
