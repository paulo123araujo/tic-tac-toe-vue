<template>
    <div class="header">
      <div class="title">
        <strong>Tic Tac Toe</strong> / <small>in VueJS</small>
      </div>
    </div>
</template>

<script>
    export default {
        name: 'Title'
    }
</script>

<style>
    .header {
      text-align: center;
      font-size: 40px;
      margin-bottom: 30px;
    }

    .header .title {
      padding-top: 50px;
      background-color: #F26B53;
      height: 100px;
      color:  #FFF;
    }
</style>