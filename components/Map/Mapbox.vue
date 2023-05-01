<!-- <template>
  
</template> -->
<template>
    <div id="mapbox-component" class="w-full h-full">
      <div ref="mapContainer" class="absolute top-0 bottom-0 w-full h-full rounded-3xl"></div>
    </div>
  </template>
  
  <script>
  import mapboxgl from 'mapbox-gl';
  import 'mapbox-gl/dist/mapbox-gl.css';
  import MapboxGeocoder from '@mapbox/mapbox-gl-geocoder';
  import 'mapbox-gl/dist/mapbox-gl.css';
  
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
      markers: {
        type: Array,
        default: () => []
      }
    },
    mounted() {
      mapboxgl.accessToken = this.accessToken;
      this.map = new mapboxgl.Map({
        container: this.$refs.mapContainer,
        style: 'mapbox://styles/mapbox/light-v11',
        center: [this.center.lng, this.center.lat],
        zoom: this.zoom
      });
  
      const geocoder = new MapboxGeocoder({
        accessToken: mapboxgl.accessToken,
        mapboxgl: mapboxgl
      });
  
      this.map.addControl(geocoder);

      //this.addMarkers();

      setTimeout(() => {
    this.addMarkers();
  }, 1000);

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
    methods: {
      addMarkers() {
        this.markers.forEach(marker => {
          const el = document.createElement('div');
          el.className = 'marker';

          const popup = new mapboxgl.Popup({ offset: 25 }).setHTML(`
            <div>
              <img src="${marker.imageUrl}" alt="${marker.title}" />
              <h2>${marker.title}</h2>
              <p>${marker.description}</p>
            </div>
          `);

          new mapboxgl.Marker(el)
            .setLngLat(marker.coordinates)
            // console.log(marker.coordinates)
            .addTo(this.map);
        });     
      }
    },
    beforeDestroy() {
      this.map.remove();
    }
  };
  </script>
  
  <style>
  .mapboxgl-canvas {
    height: 100%;
    width: 100%;
  }


  #mapbox-component .mapboxgl-marker {
    background-color : #B188EA;
    background-size: cover!important;
    width: 1.3vw!important;
    height: 1.3vw!important;
    border-radius: 50%!important;
    cursor: pointer!important;
  }
  
  </style>
  