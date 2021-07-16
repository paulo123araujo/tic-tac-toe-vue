<template>
  <div id="app">
    <Title />
    <Board v-if="canPlay()" :players="players" />
    <LoginPlayers v-else @setNewPlayers="setNewPlayers" />
  </div>
</template>

<script>
import Board from './components/Board.vue';
import LoginPlayers from './components/LoginPlayers.vue';
import Title from './components/Title.vue';

export default {
  name: 'App',
  components: {
    Board,
    LoginPlayers,
    Title
  },
  data() {
    return {
      players: []
    }
  },
  methods: {
    setNewPlayers(players) {
      if (this.isNameNotEmpty(players)) {
        this.players = players
      }
    },
    isNameNotEmpty(players) {
      for (const player of players) {
        if (player.name === "") {
          return false;
        }
      }
      return true;
    },
    canPlay() {
      if (this.players.length > 1 && this.isNameNotEmpty(this.players)) {
        return true;
      }

      return false;
    }
  }
}
</script>

<style>
body, html {
  margin: 0;
  font-family: Roboto, sans-serif;
  background-color: #ffffff;
}
</style>
