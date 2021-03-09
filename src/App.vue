<template>
  <div id="app">
    <NewsApp />
  </div>
</template>

<script>
import NewsApp from './components/NewsApp.vue'

export default {
  name: 'App',
  components: {
    NewsApp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
body{
  margin:0;
  padding: 0;
}
</style>
