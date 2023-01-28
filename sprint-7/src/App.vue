<template>
<div id="app">
  <HomeForm></HomeForm>
</div>
</template>
  
  

<script>
import HomeForm from './components/Home.vue'

export default {
  name: 'App',
  components: {
    HomeForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  margin: 0;
}
</style>
