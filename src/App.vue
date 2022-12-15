<template>
  <GoogleMap
    :api-key="apiKey"
    style="width: 100%; height: 500px"
    :center="center"
    :zoom="15"
  >
    <Marker :options="{ position: center }" />
  </GoogleMap>
  <YouTube :src="cameras" @ready="onReady" ref="youtube" />
</template>

<script setup>
import { GoogleMap, Marker } from "vue3-google-map";
import YouTube from "vue3-youtube";
import { liveCameras } from "./live-cameras";

const center = { lat: 40.689247, lng: -74.044502 };
const apiKey = import.meta.env.VITE_GOOGLE_MAP_API_KEY;
const onReady = () => {
  this.$refs.youtube.playVideo();
};
const cameras = liveCameras[0].live;
</script>
