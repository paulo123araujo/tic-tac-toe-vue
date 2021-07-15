<template>
    <div id="score">
        <div v-for="(player, index) in players" :key="index">
            <span>{{ player.name }} - wins: {{ player.winsCount }}</span>
        </div>
        <span>ties: {{ tie }}</span>
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
