<template>
    <div class="box">
        <div v-if="errors.length > 0" class="errors">
            <div v-for="(error, index) in errors" class="error" :key="index">
                {{ error }}
            </div>
        </div>
        <div class="field">
            <label for="player1">Nome do Jogador 1:</label>
            <input v-model="players[0].name" type="text" name="player1" placeholder="digite o nome do jogador 1..." />
        </div>
        <div class="field">
            <label for="player2">Nome do Jogador 2:</label>
            <input v-model="players[1].name" type="text" name="player2" placeholder="digite o nome do jogador 2..." />
        </div>
        <div class="field">
            <button type="button" @click="clickButton">Jogar</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "LoginPlayers",
    emits: ['setNewPlayers'],
    data() {
        return {
            players: [
                { name: "", winsCount: 0, current: true, value: "X" },
                { name: "", winsCount: 0, current: false, value: "O" }
            ],
            errors: []
        }
    },
    methods: {
        clickButton() {
            this.errors = [];
            if (this.isNamesNotEmpty()) {
                this.$emit('setNewPlayers', this.players)
            }
        },
        isNamesNotEmpty() {
          for (const player of this.players) {
            if (player.name === "") {
              this.setNewError("Preencha todos os nomes");
              return false;
            }
          }
          return true;
        },
        setNewError(error) {
            this.errors.push(error)
        }
    }
}
</script>

<style>
.box {
    width:  450px;
    border:  2px solid #c3c3c3;
    border-radius:  5px;
    padding: 15px;
    margin:  auto;
}

.field {
    width: 100%;
    margin: 15px auto;
}

.field label {
    color:  #373737;
    margin-right: 5px;
}

.field input {
    border:  0;
    border-bottom:  1px solid #373737;
    color: #323232;
    width:  200px;
    margin-left: 10px;
}

.field input:focus {
    border-bottom-color: #F26B53;
    transition: .5s all;
    color:  #F36B53;
}

.field button {
    width:  100%;
    border: 1px solid #c3c3c3;
    font-size: 16px;
    height:  50px;
    padding: 15px;
    background-color: #d3d3d3;
    color: #898989;
    font-weight: bold;
}

.field button:hover {
    transition: .5s all;
    background-color: #F26B53;
    color:  #fff;
}

.error {
    color: #f00;
}

</style>
