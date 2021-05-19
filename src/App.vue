<template>
  <TheDraw />
</template>

<script>
import TheDraw from './components/TheDraw';

export default {
  name: 'App',
  components: {
    TheDraw,
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
