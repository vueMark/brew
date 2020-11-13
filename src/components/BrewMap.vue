<template>
	<div class="row map">
		<!--<h2>Center is {{currentCenter}}, Zoom is {{currentZoom}}</h2>-->
		<l-map @update:zoom="zoomUpdate" @update:center="centerUpdate" :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker
		v-for="(brew,index) in brews"
		:key="index"
		:lat-lng="latlng(brew.latitude,brew.longitude)">
		<l-icon :icon-size="brew.iconSize" :icon-url="icon"></l-icon>
	</l-marker>
    </l-map>
	</div>
	<!-- /.row map -->
</template>

<script>
import L from 'leaflet';
import { LMap, LTileLayer, LMarker, LIcon } from 'vue2-leaflet';
import beer from '../assets/beer.png'

export default {
	name: "BrewMap",
	props:{
	brews:Array
},
	components: {
	LMap,
	LTileLayer,
	LMarker,
	LIcon
	},
	data(){
		return{
			zoom:6,
			center: L.latLng(34.413220, -111.219482),
			currentCenter:L.latLng(34.413220, -111.219482),
			currentZoom: 6,
			url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
			//url:'https://tile.thunderforest.com/neighbourhood/{z}/{x}/{y}.png?apikey=894f2429dea74871b58800c28f4732ea',
			attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
			marker: L.latLng(47.413220, -1.219482),
			icon: beer,
			}
  },methods:{
	latlng: function(lat,lng){
	return L.latLng(lat,lng)
  },
  zoomUpdate(zoom){
	this.currentZoom = zoom;
  },
  centerUpdate(center){
	this.currentCenter = center;
  }

  }

}
</script>

<style scoped>
.map{
	height: 100%;
}
</style>