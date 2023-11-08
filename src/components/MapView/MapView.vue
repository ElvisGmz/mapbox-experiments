<template>
  <div class="flex justify-end mb-4">
    <SearchSelect v-model="selectedCategory" />
  </div>
  <div
    class="relative w-full aspect-[3/4] sm:aspect-square md:aspect-video relative rounded-xl bg-white overflow-hidden"
  >
  <div ref="mapContainer" class="map-container w-full h-full"></div>
  <SideBar v-model="peopleList" />
  
  </div>
</template>

<script setup>
import { onMounted, ref, onUnmounted, watch } from "vue";
import SideBar from "./SideBar.vue";
import "mapbox-gl/dist/mapbox-gl.css";
import mapboxgl from "mapbox-gl";
import SearchSelect from "./SearchSelect.vue";

const selectedCategory = ref('')

mapboxgl.accessToken =
  "pk.eyJ1IjoiY2VzYXJrb2RzIiwiYSI6ImNsNzBoc2NpYzBhZnYzdW8zd2pjNTdkamwifQ.0G9m35T_Emzep17V43q9Ug";

const geojson = {
  type: "FeatureCollection",
  features: [
    {
      type: "Feature",
      geometry: {
        type: "Point",
        coordinates: [-77.032, 38.913],
      },
      properties: {
        id: "id-1",
        title: "Mapbox",
        description: "Washington, D.C.",
        counter: 10,
        category: 'category-1',
        people: [
          {
            name: "Elvis",
            last_name: "Gomez",
            avatar: "URL_de_la_imagen_de_Elvis",
            logo: "URL_del_logo_de_Elvis",
            description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam? Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Elvis" },
              { platform: "Instagram", link: "URL_de_instagram_de_Elvis" },
              // Puedes agregar más plataformas sociales si es necesario
            ],
            categories: [
              { name: "categoria1", link: "URL_categoria1" },
              { name: "categoria2", link: "URL_categoria2" },
              // Puedes agregar más categorías si es necesario
            ],
          },
          {
            name: "Cesar",
            last_name: "Ramirez",
            avatar: "URL_de_la_imagen_de_Cesar",
            logo: "URL_del_logo_de_Cesar",
            description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Cesar" },
              { platform: "Instagram", link: "URL_de_instagram_de_Cesar" },
            ],
            
          },
          {
            name: "Evan",
            last_name: "You",
            avatar: "URL_de_la_imagen_de_Evan",
            logo: "URL_del_logo_de_Evan",
            description: "",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Evan" },
              { platform: "Instagram", link: "URL_de_instagram_de_Evan" },
            ],
            
          },
        ],
      },
    },
    {
      type: "Feature",
      geometry: {
        type: "Point",
        coordinates: [-77.082, 38.973],
      },
      properties: {
        id: "id-2",
        title: "Mapbox",
        description: "San Francisco, California",
        counter: 5,
        category: 'category-2',
        people: [
          {
            name: "Elvis",
            last_name: "Gomez",
            avatar: "URL_de_la_imagen_de_Elvis",
            logo: "URL_del_logo_de_Elvis",
            description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Elvis" },
              { platform: "Instagram", link: "URL_de_instagram_de_Elvis" },
              // Puedes agregar más plataformas sociales si es necesario
            ],
            categories: [
              { name: "categoria1", link: "URL_categoria1" },
              { name: "categoria2", link: "URL_categoria2" },
              // Puedes agregar más categorías si es necesario
            ],
          },
          {
            name: "Cesar",
            last_name: "Ramirez",
            avatar: "URL_de_la_imagen_de_Cesar",
            logo: "URL_del_logo_de_Cesar",
            description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Cesar" },
              { platform: "Instagram", link: "URL_de_instagram_de_Cesar" },
            ],
            
          },
          {
            name: "Evan",
            last_name: "You",
            avatar: "URL_de_la_imagen_de_Evan",
            logo: "URL_del_logo_de_Evan",
            description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At exercitationem rerum nulla dignissimos temporibus voluptatum tenetur accusamus sequi fugiat laudantium. Nulla, placeat atque a nihil ea fugit deleniti inventore numquam?",
            socials: [
              { platform: "Facebook", link: "URL_de_facebook_de_Evan" },
              { platform: "Instagram", link: "URL_de_instagram_de_Evan" },
            ],
            
          },
        ],
      },
    },
  ],
};

const mapRef = ref(null);
const mapContainer = ref();
const peopleList = ref(null);

onMounted(() => {
  const map = new mapboxgl.Map({
    container: mapContainer.value,
    style: "mapbox://styles/mapbox/streets-v12", // Replace with your preferred map style
    center: [-77.032, 38.913],
    zoom: 9,
  });

  const popup = new mapboxgl.Popup({
    closeButton: false,
    closeOnClick: false,
    offset: [0, -20]
    });


  // add markers to map
  for (const feature of geojson.features) {
    // create a HTML element for each feature
    const el = document.createElement("div");
    el.className = "marker";
    el.textContent = feature.properties.counter;

    // make a marker for each feature and add to the map
    const marker = new mapboxgl.Marker(el)
      .setLngLat(feature.geometry.coordinates)
      .addTo(map);

      marker.getElement().addEventListener("click", () => {
      // Access the properties data of the clicked marker
      console.log(feature.properties);
      peopleList.value = feature.properties.people;
    });

    marker.getElement().addEventListener("mouseover", () => {
      // Access the properties data of the clicked marker
      popup.setLngLat(feature.geometry.coordinates).setHTML(feature.properties.description).addTo(map);
    });

    marker.getElement().addEventListener("mouseleave", () => {
      popup.remove();
    })
  }

  mapRef.value = map;
});

onUnmounted(() => {
  mapRef.value.remove();
  mapRef.value = null;
});

watch(selectedCategory, (newValue) => {
  const mapInstance = mapRef.value;

  if (mapInstance) {
    let filteredFeatures = geojson.features;

    if (newValue !== '') {
      filteredFeatures = geojson.features.filter(feature => feature.properties.category === newValue);
    }

    const newGeoJSON = {
      type: 'FeatureCollection',
      features: filteredFeatures
    };

    // Remove all existing markers
    const markers = document.getElementsByClassName('marker');
    while (markers[0]) {
      markers[0].parentNode.removeChild(markers[0]);
    }

    // Add markers for the filtered features
    for (const feature of filteredFeatures) {
      const el = document.createElement('div');
      el.className = 'marker';
      el.textContent = feature.properties.counter;

      const marker = new mapboxgl.Marker(el)
        .setLngLat(feature.geometry.coordinates)
        .addTo(mapInstance);

      marker.getElement().addEventListener('click', () => {
        peopleList.value = feature.properties.people;
      });
    }

    const geojsonSource = mapInstance.getSource('markers'); // Assuming you've named your source 'markers'
    if (geojsonSource) {
      geojsonSource.setData(newGeoJSON);
    } else {
      mapInstance.addSource('markers', {
        type: 'geojson',
        data: newGeoJSON
      });

      mapInstance.addLayer({
        id: 'markers',
        type: 'symbol',
        source: 'markers',
        layout: {
          'icon-image': 'marker-15', // Customize this according to your needs
          'text-field': '{counter}',
          'text-size': 12
        }
      });
    }
  }
});
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

.mapboxgl-popup-content {
  padding: 10px 8px;
  border-radius: 4px;
  overflow: hidden;
  max-width: 100px;
  text-align: center;
}

</style>
