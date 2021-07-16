<template>
    <span>Vez do jogador: <strong>{{ currentPlayer.name }}</strong></span>
</template>

<script>
    export default {
        name: 'CurrentPlayer',
        props: {
            players: {
                type: [],
                default: [],
            }
        },
        computed: {
            currentPlayer() {
                return this.players.filter(player => player.current)[0]
            }
        }
    }
</script>

<style>
    span {
        text-align: center;
        font-size: 32px;
    }
</style>