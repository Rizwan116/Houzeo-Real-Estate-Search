<template>
  <div id="map" style="width: 100%; height: 100%;"></div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';

const map = ref(null);

onMounted(() => {
  map.value = L.map('map').setView([37.7749, -122.4194], 10); // Default location (San Francisco)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
  }).addTo(map.value);

  // Example marker
  L.marker([37.7749, -122.4194]).addTo(map.value)
    .bindPopup('San Francisco')
    .openPopup();
});
</script>

<style scoped>
#map {
  width: 100%;
  height: 400px; /* Adjust height as needed */
}
</style>
