<template>
  <div id="app">
    <client-form />
  </div>
</template>

<script>
import clientForm from './components/clientForm.vue'

export default {
  name: 'App',
  components: {
    clientForm,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400&display=swap');
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #b8c6db;
  height: 100vh;

}
</style>
