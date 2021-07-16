<template>
  <div id="app">
    <div class="header">
      <div class="title">
        <strong>Tic Tac Toe</strong> / <small>in VueJS</small>
      </div>
    </div>
    <Board v-if="canPlay()" :players="players" />
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

.header {
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
}

.header .title {
  padding-top: 50px;
  background-color: #F26B53;
  height: 100px;
  color:  #FFF;
}
</style>
