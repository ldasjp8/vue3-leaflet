<template>
  <div>
    <ul>
      <li>Latitude (North): {{lat1}}</li>
      <li>Longitude (West): {{lng1}}</li>
      <li>Latitude (South): {{lat2}}</li>
      <li>Longitude (East): {{lng2}}</li>
    </ul>
  </div>
  <div style="height: 400px; width: 100%">
    <l-map
      ref="map"
      :center="[35.68944, 139.69167]"
      :zoom="15"
      @ready="init"
      @update:bounds="showBounds"
    >
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></l-tile-layer>
      <l-control-layers />
    </l-map>
  </div>
</template>
<script>
import { LMap, LTileLayer, LControlLayers } from '@vue-leaflet/vue-leaflet'
import 'leaflet/dist/leaflet.css'

export default {
  components: {
    LMap,
    LTileLayer,
    LControlLayers
  },
  data() {
    return {
      lat1 : 0,
      lng1 : 0,
      lat2: 0,
      lng2: 0
    }
  },
  methods: {
    init(){
      const map = this.$refs.map.leafletObject
      this.showBounds(map.getBounds())
    },
    showBounds (bounds) {
      const posNW = bounds.getNorthWest()
      const posSE = bounds.getSouthEast()
      this.lat1 = posNW.lat
      this.lng1 = posNW.lng
      this.lat2 = posSE.lat
      this.lng2 = posSE.lng
    }
  }
}
</script>
