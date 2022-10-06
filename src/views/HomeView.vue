<template>
  <div class="home">

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>

<style>
  .home {
    width: 480px;
    height: auto;
    margin: 0 auto;

    border: 1px solid black;
  }
</style>