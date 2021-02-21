<template>
  <div id="app">
    <Navbar />
    <router-view></router-view>
    
    <Footer />
  </div>

</template>

<script>
import Navbar from './components/layout/Navbar.vue'
import Footer from './components/layout/Footer.vue'

export default {
  name: 'App',
  components: {
    Navbar, Footer
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap");

html, #app {
  font-family: 'Roboto';
  color: #2c3e50;  
  margin: 60px;
}

.search-bar {
  display: block;
  margin: auto;
  margin-top: 30px;
  text-align: center;
}

/* #app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 60px;
} */

.btn {
    display: inline-block;
    border: none;
    background: rgb(206, 124, 124);
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: rgb(218, 85, 81);
  }
</style>
