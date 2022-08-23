<template>
  <div id="app">
    <img src="./assets/logo.png">
    <nav>
      <ul>
        <li> <router-link to="/">Home</router-link> </li>
        <li> <router-link to="/numbers">1 2 3</router-link> </li>
      </ul>
    </nav>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
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
nav li {
  display: inline-block;
  margin: 5px;
}
</style>
