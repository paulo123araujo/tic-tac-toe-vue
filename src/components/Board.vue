<template>
    <div id="board">
        <span>Vez do jogador: <strong>{{ currentPlayer.name }}</strong></span>
        <div class="game-board">
            <div 
                v-for="(square, index) in game.board"
                :key="index"
                class="square"
                @click="doMove(index)"
            >
                <span>{{ square }}</span>
            </div>
        </div>
    </div>
    <button type="button" @click="newGame()">Novo Jogo</button>
    <PlayersScore :players="players" :tie="tieCount"/>
</template>

<script>
import PlayersScore from './PlayersScore.vue'

export default {
    name: "Board",
    components: {
        PlayersScore
    },
    data() {
        return {
            players: [
                { name: "player 1", winsCount: 0, current: true, value: "X" },
                { name: "player 2", winsCount: 0, current: false, value: "O" }
            ],
            game: {
                number: 1,
                board: ["", "", "", "", "", "", "", "", ""],
                finished: false,
                winner: ""
            }
        }
    },
    computed: {
        currentPlayer() {
            return this.players.filter(player => player.current)[0]
        },
        tieCount() {
            return this.game.number > 1 
            ? this.game.number - (this.players[0].winsCount + this.players[1].winsCount) 
            : 0
        }
    },
    methods: {
        newGame() {
            for (let i = 0; i < this.game.board.length; ++i) {
                this.game.board[i] = "";
            }

            this.game.finished = false;
            this.game.winner = "";
            this.setNewCurrentPlayer();
            ++this.game.number
        },
        doMove(index) {
            if (this.game.finished) {
                return;
            }

            if (this.game.board[index] !== "") {
                return
            }

            this.game.board[index] = this.currentPlayer.value;
            this.checkWinner();
        },
        checkWinner() {
            if (this.checkHorizontal()) {
                this.setWinner()
                return;
            }

            if (this.checkVertical()) {
                this.setWinner();
                return;
            }

            if (this.checkDiagonal()) {
                this.setWinner()
                return;
            }
            this.setNewCurrentPlayer();
            return
        },
        setNewCurrentPlayer() {
            if (this.players[0].current) {
                this.players[0].current = false;
                this.players[1].current = true;
                return;
            }

            this.players[0].current = true;
            this.players[1].current = false;
        },
        checkHorizontal() {
            return (this.game.board[0] === this.game.board[1]
                && this.game.board[1] === this.game.board[2]
                && this.game.board[0] !== "")
                || (this.game.board[3] === this.game.board[4]
                && this.game.board[4] === this.game.board[5]
                && this.game.board[3] !== "")
                || (this.game.board[6] === this.game.board[7]
                && this.game.board[7] === this.game.board[8]
                && this.game.board[6] !== "");
        },
        checkVertical() {
            return (this.game.board[0] === this.game.board[3]
                && this.game.board[3] === this.game.board[6]
                && this.game.board[0] !== "")
                || (this.game.board[1] === this.game.board[4]
                && this.game.board[4] === this.game.board[7]
                && this.game.board[1] !== "")
                || (this.game.board[2] === this.game.board[5]
                && this.game.board[5] === this.game.board[8]
                && this.game.board[2] !== "")
        },
        checkDiagonal() {
            return (this.game.board[0] === this.game.board[4]
                && this.game.board[4] === this.game.board[8]
                && this.game.board[0] !== "")
                || (this.game.board[2] === this.game.board[4]
                && this.game.board[4] === this.game.board[6]
                && this.game.board[2] !== "");
        },
        setWinner() {
            this.game.finished = true;
            ++this.currentPlayer.winsCount;
            this.game.winner = this.currentPlayer.name;
            window.alert(`Jogador ${this.game.winner} venceu!\nJogue novamente!`);
        }
    }
}
</script>

<style>
.game-board {
    width: 600px;
	height: 600px;
	margin: 0 auto;
    background-color: #34495e;
    color: #fff;
    border: 6px solid #2c3e50;
    border-radius: 10px;
	
	display: grid;
	grid-template: repeat(3, 1fr) / repeat(3, 1fr);
}

.square {
    border: 6px solid #2c3e50;
    border-radius: 2px;
    font-family: Helvetica;
    font-weight: bold;
    font-size: 4em;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
