<template>
   <div id="app">
  <!-- added a navbar -->
   <nav class="navbar navbar-dark bg-dark">
     <span class="navbar-brand mb-0 h2">GitHub Download Stats</span>
     <a href="https://aveek-saha.github.io/" class="navbar-brand mb-0 h1 text-right">
       <i class="fab fa-github fa-inverse"></i>
     </a>
   </nav>

   <!-- wrapped the data component in a container -->
   <div class="container">
   <!-- inject the Data component -->
     <Data/>
   </div>

 </div>
</template>

<script>
import Data from './components/Data.vue'

export default {
  name: 'App',
  components: {
    Data
  }
}
</script>

<style>
  /* global styles */
body{
    background-color: #FEFEFE
}

.asset{
    word-break: break-all;
}

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
}
</style>
