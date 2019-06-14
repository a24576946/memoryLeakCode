<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h2 @click="toNewPages">打开新页面</h2>    
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  methods:{
    toNewPages(){
      window.location.href = 'http://localhost:8080/test.html'
    }
  }  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
