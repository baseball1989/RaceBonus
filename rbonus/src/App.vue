<template>
  <RootPage />
</template>

<script>
import RootPage from './components/RootPage.vue'

export default {
  name: 'App',
  components: {
    RootPage
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
