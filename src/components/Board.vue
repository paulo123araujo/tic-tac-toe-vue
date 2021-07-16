<template>
    <div id="board">
        <CurrentPlayer :players="playersData"/>
        <div class="game-board">
            <Square 
                v-for="(square, index) in game.board"
                :key="index"
                @click="doMove(index)"
                :squareValue="square"
            />
        </div>
    </div>
    <NewGameButton @newGame="newGame" />
    <PlayersScore :players="players" :tie="tieCount"/>
</template>

<script>
import PlayersScore from './PlayersScore.vue';
import Square from './Square.vue';
import NewGameButton from './NewGameButton';
import CurrentPlayer from './CurrentPlayer.vue';

export default {
    name: "Board",
    components: {
        PlayersScore,
        Square,
        NewGameButton,
        CurrentPlayer
    },
    props: {
        players: {
            required: true,
            type: Array
        }
    },
    data() {
        return {
            playersData: this.players,
            game: {
                number: 1,
                board: ["", "", "", "", "", "", "", "", ""],
                finished: false,
                winner: ""
            }
        }
    },
    computed: {
        tieCount() {
            let tie = 0;
            if (this.game.number > 1) {
                tie = this.game.number - (this.players[0].winsCount + this.players[1].winsCount)
                tie = (!this.game.finished) ? tie - 1 : tie;
            }
            return tie;
        }
    },
    methods: {
        getCurrentPlayer() {
            return this.playersData.filter(player => player.current)[0]
        },
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

            const currentPlayer = this.getCurrentPlayer();

            this.game.board[index] = currentPlayer.value;
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
            if (this.playersData[0].current) {
                this.playersData[0].current = false;
                this.playersData[1].current = true;
                return;
            }

            this.playersData[0].current = true;
            this.playersData[1].current = false;
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

            const currentPlayer = this.getCurrentPlayer();

            this.game.winner = currentPlayer.name;
            alert(`Jogador ${this.game.winner} venceu!\nJogue novamente!`);
        }
    }
}
</script>

<style>
#board {
    width:  100%;
    text-align: center;
}

.game-board {
    width: 400px;
	height: 400px;
	margin: 0 auto;
    margin-top: 35px;
    background-color: #34495e;
    color: #fff;
    border: 6px solid #2c3e50;
    border-radius: 10px;
	
	display: grid;
	grid-template: repeat(3, 1fr) / repeat(3, 1fr);
}
</style>
