<template>
  <Nav />
  <SearchBar />
  <Properties />

</template>

<script>
import Nav from './components/Nav.vue'
import SearchBar from './components/SearchBar.vue';
import Properties from './components/Properties.vue';



export default {
  name: 'App',
  components: {
    Nav,
    SearchBar,
    Properties
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  
}
body {
  
}
#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow: hidden;
}
</style>
