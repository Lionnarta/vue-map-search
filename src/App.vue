<template>
  <div class="app-container">
    <div id="app">
      <Search @searchContent="searchLocation"/>
      <Map ref="maps"/>
    </div>
  </div>
</template>

<script>
import Map from './components/Maps.vue';
import Search from './components/Search.vue';
import L from 'leaflet';

export default {
  name: 'App',
  components: {
    Map,
    Search
  },
  data() {
    return {
      marker: null
    }
  },
  methods: {
    searchLocation(obj) {
      var maps = this.$refs['maps'].map;
      if (this.marker) {
        maps.removeLayer(this.marker);
      }
      this.marker = new L.marker([obj.geometry.coordinates[1], obj.geometry.coordinates[0]]);
      maps.addLayer(this.marker);
      maps.fitBounds([[obj.bbox[1], obj.bbox[0]], [obj.bbox[3], obj.bbox[2]]])
    }
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
  }
</style>
