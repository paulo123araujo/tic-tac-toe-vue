<template>
    <div class="button">
        <button type="button" @click="$emit('newGame')">Novo Jogo</button>
    </div>
</template>

<script>
    export default {
        name: 'NewGameButton',
        emits: ['newGame']
    }
</script>

<style>
    .button {
        width: 100%;
        margin: 0 auto;
    }

    .button button[type="button"] {
        border: 1px solid #434343;
        padding: 15px;
        background-color: #e3e3e3;
        color:  #333333;
        border-radius: 8px;
        width: 300px;
        margin: 50px;
        cursor: pointer;
        font-weight: bold;
    }

    .button button[type="button"]:hover {
        background-color: #333333;
        color: #e3e3e3;
        transition:  .5s all;
    }
</style>