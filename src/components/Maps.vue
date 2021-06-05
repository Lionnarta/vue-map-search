<template>
  <div id="map"></div>
</template>

<script>
import L from 'leaflet'
export default {
  data() {
    return {
      map: null,
      center: [0.7893, 118.9213],
      zoom: 5,
      token: "pk.eyJ1IjoibGlvbm5hcnRhIiwiYSI6ImNrcDN5ZG1vZjFmNjcyb213aWI0eDFxZ3EifQ.3ZDlqLIg1ssG-uYeYZtWSA"
    }
  },
  mounted() {
    this.map = L.map("map", {
      center: this.center,
      zoom: this.zoom
    });

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 19,
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    }).addTo(this.map);

    this.map.zoomControl.setPosition('bottomright');
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #map {
    position: relative;
    width: 100vw;
    height: 100vh;
  }
</style>
