<template>
    <div class="box">
        <div class="field">
            <input type="text" placeholder="digite o nome do jogador 1..." />
            <input type="text" placeholder="digite o nome do jogador 2..." />
            <button type="button">Jogar</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "LoginPlayers",
    data() {
        return {
            players: []
        }
    }
}
</script>
