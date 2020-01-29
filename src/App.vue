<template>
  <div id="app">
    <Main></Main>
  </div>
</template>

<script>

import Main from "@/components/Main";
export default {
  name: 'app',
  components: {
    Main

  }
}
</script>

<style>
  * {
    margin: 0;
    outline: none;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 15px;
  }
</style>
