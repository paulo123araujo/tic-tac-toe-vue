<template>
    <div class="box">
        <div class="field">
            <input type="text" placeholder="digite o nome do jogador 1..." v-model="players[0].name" />
            <input type="text" placeholder="digite o nome do jogador 2..." v-model="players[1].name" />
            <button type="button" @click="$emit('setNewPlayers', players)">Jogar</button>
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
            ]
        }
    },
    methods: {

    }
}
</script>
