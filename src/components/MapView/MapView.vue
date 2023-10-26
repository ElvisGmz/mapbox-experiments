<template>
  <div class="relative w-full aspect-video relative rounded-xl bg-white overflow-hidden">
    <div ref="mapContainer" class="map-container w-full h-full"></div>
    <SideBar v-model="peopleList" />
  </div>
</template>
  
<script setup>
import { onMounted, ref, onUnmounted } from 'vue'
import SideBar from './SideBar.vue'
import "mapbox-gl/dist/mapbox-gl.css"
import mapboxgl from "mapbox-gl";

mapboxgl.accessToken = "pk.eyJ1IjoiY2VzYXJrb2RzIiwiYSI6ImNsNzBoc2NpYzBhZnYzdW8zd2pjNTdkamwifQ.0G9m35T_Emzep17V43q9Ug"

const geojson = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.032, 38.913]
      },
      properties: {
        id: 'id-1',
        title: 'Mapbox',
        description: 'Washington, D.C.',
        counter: 10,
        people: [
          {
            name: 'Elvis',
            last_name: 'Gomez',
          },
          {
            name: 'Cesar',
            last_name: 'Ramirez',
          },
          {
            name: 'Evan',
            last_name: 'You',
          },
        ]
      }
    },
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.082, 38.973]
      },
      properties: {
        id: 'id-2',
        title: 'Mapbox',
        description: 'San Francisco, California',
        counter: 5,
        people: [
          {
            name: 'Mark',
            last_name: 'Zucaritas',
          },
          {
            name: 'Cesar',
            last_name: 'Ramirez',
          },
          {
            name: 'Elon',
            last_name: 'Musk',
          },
        ]
      }
    }
  ]
};

const mapRef = ref(null)
const mapContainer = ref()
const peopleList = ref(null)

onMounted(() => {
  const map = new mapboxgl.Map({
    container: mapContainer.value,
    style: "mapbox://styles/mapbox/streets-v12", // Replace with your preferred map style
    center: [-77.032, 38.913],
    zoom: 9,
  });

  // add markers to map
  for (const feature of geojson.features) {
    // create a HTML element for each feature
    const el = document.createElement('div');
    el.className = 'marker';
    el.textContent = feature.properties.counter


    // make a marker for each feature and add to the map
    const marker = new mapboxgl.Marker(el).setLngLat(feature.geometry.coordinates).addTo(map);

    marker.getElement().addEventListener('click', () => {
      // Access the properties data of the clicked marker
      console.log(feature.properties);
      peopleList.value = feature.properties.people
    });
  }

  mapRef.value = map
})

onUnmounted(() => {
  mapRef.value.remove()
  mapRef.value = null
})


</script>
  
<style>
.map-container {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  flex: 1;
}

.mapboxgl-marker {
  cursor: pointer;
}

.marker {
  background-color: #015a96;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}
</style>