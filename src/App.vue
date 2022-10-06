<template>
  <div class="wrapper">
    <nav>
      <Weather />
      <!-- <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> -->
      </nav>
      <router-view/>
    </div>
</template>

<script>

import Weather from './components/Weather.vue';
export default {
  components:{
    Weather
}
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  padding: 0;
  margin: 0;
}
.wrapper {
  width: 480px;
  margin: 0 auto;
}

nav {
  // padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
