<!-- <template>
  
</template> -->
<template>
    <div class="w-full h-full">
      <div ref="mapContainer" class="absolute top-0 bottom-0 w-full h-full"></div>
    </div>
  </template>
  
  <script>
  import mapboxgl from 'mapbox-gl';
  import 'mapbox-gl/dist/mapbox-gl.css';
  import MapboxGeocoder from '@mapbox/mapbox-gl-geocoder';
  // import MapboxMarkers from 'mapbox-gl-markers';
  // import { MapboxMarker } from 'mapbox-gl-markers';
  
  export default {
    name: 'Mapbox',
    props: {
      accessToken: {
        type: String,
        required: true
      },
      center: {
        type: Object,
        required: true
      },
      zoom: {
        type: Number,
        default: 13
      },
      // markers: {
      //   type: Array,
      //   required: true
      // }
    },
    mounted() {
      mapboxgl.accessToken = this.accessToken;
      this.map = new mapboxgl.Map({
        container: this.$refs.mapContainer,
        style: 'mapbox://styles/mapbox/streets-v11',
        center: [this.center.lng, this.center.lat],
        zoom: this.zoom
      });
  
      const geocoder = new MapboxGeocoder({
        accessToken: mapboxgl.accessToken,
        mapboxgl: mapboxgl
      });
  
      this.map.addControl(geocoder);

      // const markers = new MapboxMarkers();
      //   this.markers.forEach(marker => {
      //   markers.addMarker(marker);
      //   });
      //   markers.addMarkersToMap(this.map);
  
      // markers.setMarkers(this.markers);
  
      // this.map.on('load', () => {
      //   markers.addMarkersToMap(this.map);
      // });
    },
    beforeDestroy() {
      this.map.remove();
    }
  };
  </script>
  
  <style scoped>
  .mapboxgl-canvas {
    height: 100%;
    width: 100%;
  }
  </style>
  