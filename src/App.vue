<template>
  <Draw />
</template>

<script>
import Draw from './components/Draw';

export default {
  name: 'App',
  components: {
    Draw,
  }
}
</script>

<style>
  * {
    padding: 0;
    margin: 0;
  }

  #app {
    font-family: Open Sans, Helvetica, Arial, sans-serif;
  }
</style>
