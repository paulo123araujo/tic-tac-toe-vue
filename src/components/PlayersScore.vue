<template>
    <div id="score">
        <div v-for="(player, index) in players" :key="index">
            <span><strong>{{ player.name }}</strong> - Vitórias: <strong>{{ player.winsCount }}</strong></span>
        </div>
        <span>Empates: <strong>{{ tie }}</strong></span>
    </div>
</template>

<script>
export default {
    name: "PlayersScore",
    props: {
        players: {
            type: Array,
            required: true
        },
        tie: {
            type: Number,
            default: 0
        }
    }
}
</script>

<style>
    #score {
        width:  450px;
        padding-top: 30px;
        padding-bottom: 30px;
        border:  2px solid #34495e;
        text-align: center;
        margin: 0 auto;
        margin-bottom: 100px;
        background-color: #f3f3f3;
        border-radius: 8px;
    }
</style>
