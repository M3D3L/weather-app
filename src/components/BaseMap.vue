<template>
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

  data() {
    return {

    };
  },
};
</script>
