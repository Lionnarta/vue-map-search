<template>
  <div class="app-container">
    <div id="app">
      <Search/>
      <Map/>
    </div>
  </div>
</template>

<script>
import Map from './components/Maps.vue';
import Search from './components/Search.vue';

export default {
  name: 'App',
  components: {
    Map,
    Search
  }
}
</script>

<style>
  * {
    margin: 0;
    box-sizing: border-box;
  }
  .app-container {
    position: relative;
  }
  #app {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }
</style>
