<template>
    
    <div>
    <!-- Other properties content -->

    <div class="properties-container">
      <div class="map-container" style="width: 50%;">
      <MapComponent />
    </div>
    <div class="property-listing">
      <PropertyListings />
    </div>
    </div>

    <!-- Mobile CTA for Map -->
    <div v-if="isMobile" class="map-cta" @click="openMap">
      <span>Map</span>
      <font-awesome-icon :icon="['fas', 'map']" />
    </div>

    <!-- Popup for Leaflet Map -->
    <transition name="fade">
      <div v-if="showMap" class="map-popup" @click.self="closeMap">
        <div class="map-container">
          <button class="close-button" @click="closeMap">X</button> <!-- Close button -->
          <leaflet-map :center="mapCenter" :zoom="mapZoom" />
        </div>
      </div>
    </transition>
  </div>

    
  </template>
  
  <script setup>
  import MapComponent from './MapComponent.vue';
  import PropertyListings from './PropertyListings.vue';
  import { ref, computed } from 'vue';
  import { library } from '@fortawesome/fontawesome-svg-core';
  import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
  import { faMap } from '@fortawesome/free-solid-svg-icons';

library.add(faMap);

const showMap = ref(false);
const mapCenter = ref([37.7749, -122.4194]); // Example coordinates
const mapZoom = ref(13);

const isMobile = computed(() => {
  return window.innerWidth <= 768; // Adjust this as necessary
});

const openMap = () => {
  showMap.value = true;
};

const closeMap = () => {
  showMap.value = false;
};
  
  
  </script>
  
  <style scoped>
  .properties-container {
    display: flex;
    width: 100%;
  }
  .property-listing {
    width: 50%;
  }

  .map-cta {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  background-color: #0B5AA5;
  color: white;
  border-radius: 30px;
  padding: 15px 20px;
  display: flex;
  align-items: center;
  gap: 5px;
  cursor: pointer;
  z-index: 1000;
}

.map-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
}

.map-container {
  width: 90%;
  height: 90%;
  background: white;
  border-radius: 8px;
  overflow: hidden;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.close-button {
  position: absolute;
  top: 25px; /* Adjust position */
  right: 8px; /* Adjust position */
  background: #0B5AA5; /* Background color for the button */
  color: white; /* Text color */
  border: none;
  border-radius: 50%; /* Fully rounded */
  width: 30px; /* Button width */
  height: 30px; /* Button height */
  cursor: pointer; /* Pointer cursor on hover */
  font-size: 16px; /* Font size */
  z-index: 2000; /* Ensure it's on top of other elements */
}

/* Adjustments for responsive layout */
@media (max-width: 768px) {
  .properties-container {
    flex-direction: column; /* Stack components vertically on smaller screens */
  }
  .property-listing {
    width: 100%;
  }
}
  
  /* Adjustments for responsive layout */
  @media (max-width: 768px) {
    .properties-container {
      flex-direction: column; /* Stack components vertically on smaller screens */
    }
    .property-listing {
      width: 100%;
    }
  }
  </style>
  