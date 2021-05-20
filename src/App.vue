<template>
<!-- component -->
<div class="flex flex-wrap items-center max-h-full md">
      <div class="flex justify-center w-full h-screen text-center bg-white">
        <div>

          <!-- country region island -->
          <div class="flex w-full font-light text-gray-500 bg-gray-600">
              <div class="py-3 bg-red-400 border search-box">
                <div class="px-3 py-6 text-3xl text-white">Type City Name</div>
            <input type="text px-2 " 
            class="search-bar" 
            placeholder="" 
            v-model="query"
            @keypress="fetchWeather">
          <h1 class="text-6xl font-bold text-black">{{ query }}</h1>

          <div class="pr-4 " v-if="typeof weather.main != 'undefined'">
            <!-- description -->
          <div 
            class="w-full px-16 py-6 mt-16 text-lg text-white lg:text-lg description">
            {{ weather.weather[0].main }} today in {{ query }}, {{ weather.sys.country }}. Expect lows of 
            {{ Math.round(weather.main.temp_min) }} and highs of {{ Math.round(weather.main.temp_max)}}.

            
          </div>

            <div style="height: 100vh; width: 100vw;">
    <l-map
      v-model="zoom"
      v-model:zoom="zoom"
      :center= center
    >
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png"
      ></l-tile-layer>
      <l-marker  :lat-lng= markerLatLng >
      </l-marker>
    </l-map>
  </div>
              </div>
          
          </div>
          
          </div>
          
        </div>
      </div>
    </div>

</template>
<script>
import {
  LMap,
  LIcon,
  LTileLayer,
  LMarker,
  LControlLayers,
  LTooltip,
  LPopup,
  LPolyline,
  LPolygon,
  LRectangle,
} from "@vue-leaflet/vue-leaflet";
import "leaflet/dist/leaflet.css";
export default {
  setup(){

  },

  components: {
    LMap,
    LIcon,
    LTileLayer,
    LMarker,
    LControlLayers,
    LTooltip,
    LPopup,
    LPolyline,
    LPolygon,
    LRectangle,
  },
  
  name: 'app',
  data() {
    return {
      api_key: '3edfbd357c702951d7d8132f7a587e1e',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      zoom: 2.5,
      markerLatLng: [`this.weather.coord.lat, this.weather.coord.lon`],
      center: [50, -115]
    }
  },
  methods:{
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
      this.markerLatLng= [results.coord.lat, results.coord.lon];


    }
  },
}
</script>

