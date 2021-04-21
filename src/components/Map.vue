<template>
<div class="wrapper">
  <h1>{{nameOfCity}}</h1>
  <l-map class="map" :zoom="zoom" :center="center" >
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <l-marker v-for="marker, index in markers" v-on:click="chooseCity(cities[index].name)" v-bind:key="index" :icon="icon" :lat-lng="marker">
      <l-popup>{{cities[index].name}} {{cities[index].coordinates}}</l-popup>
    </l-marker>
  </l-map>
</div>
</template>

<script>

import L, { icon } from 'leaflet';
import { LMap, LTileLayer, LMarker, LPopup} from 'vue2-leaflet';
import 'leaflet/dist/leaflet.css';

export default {
  name: 'Map',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup
  },
   data() {
    return {
      zoom: 5,
      center: L.latLng(50.4547, 30.5238),
      url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      markers: [],
      nameOfCity: 'Місто ще не обране',
      cities: [
        {
          name:"Київ",
          coordinates: [50.4547, 30.5238]
        },
        {
          name:"Дніпро",
          coordinates: [48.4593, 35.0387]
        },
        {
          name:"Львів",
          coordinates: [49.8383, 24.0232]
        },
        {
          name:"Донецьк",
          coordinates: [48.023, 37.8022]
        },
        {
          name:"Одеса",
          coordinates: [46.4775, 30.7326]
        }
      ],
      icon: icon({
        iconUrl: "https://simpleicon.com/wp-content/uploads/map-marker-1.png",
        iconSize: [32, 37],
        iconAnchor: [16, 37]
      }),
      staticAnchor: [16, 37],
      customText: "Foobar",
      iconSize: 64
    }
  },
   methods: {
     chooseCity(cityName) {
       this.nameOfCity = cityName;
       console.log(this.nameOfCity);
     }
  },
  beforeMount() {
    this.cities.forEach(city => {
      this.markers.push(L.latLng(city.coordinates[0], city.coordinates[1]));
    })
  }
};

</script>

<style>
  .wrapper{
    height: 100%;
  }
  .map{
    display: flex;
    height: 90%;
  }
</style>