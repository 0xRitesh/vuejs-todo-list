<template>
  <div id="app">
    <Topself />
    <Header />
    <router-view/>
  </div>
</template>

<script>

import Header from './components/header'
import Topself from './components/topself.vue'

export default {
  name: 'App',
  components: {
    Header,
    Topself
}
}
</script>

<style>
  #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  }

  #nav {
    padding: 15px;
    text-align: center;
  }

  #nav a {
    font-weight: bold;
    color: #2c3e50;
    margin: 0 10px;
    text-decoration: none;
  }

  #nav a.router-link-exact-active {
    color: #42b983;
  }
</style>
