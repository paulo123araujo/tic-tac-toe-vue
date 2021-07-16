<template>
    <div class="square">
        <span>{{ squareValue }}</span>
    </div>
</template>

<script>
    export default {
        name: 'Square',
        props: {
            squareValue: {
                default: '',
                type: String
            }
        }
    }
</script>

<style>
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