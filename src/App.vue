<template>
  <GoogleMap
    :api-key="apiKey"
    style="width: 100%; height: 500px"
    :center="center"
    :zoom="4"
  >
    <Marker
      v-for="camera in cameras"
      :options="{ position: { lat: camera.lat, lng: camera.lng } }"
      @click="showModal()"
    />
  </GoogleMap>

  <video-modal :isVisible="modalVisible" @close="closeModal">
    <YouTube
      :src="'https://www.youtube.com/watch?v=jNQXAC9IVRw&t=11s'"
      @ready="onReady"
      ref="youtube"
    />
  </video-modal>
</template>

<script setup>
import { ref } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";
import YouTube from "vue3-youtube";
import { liveCameras } from "./live-cameras";
import videoModal from "./components/videoModal.vue";

const center = { lat: 38.0, lng: 140.0 };
const apiKey = import.meta.env.VITE_GOOGLE_MAP_API_KEY;
const onReady = () => {
  this.$refs.youtube.playVideo();
};
const cameras = liveCameras;

let modalVisible = ref(false);
const showModal = () => {
  modalVisible.value = true;
};
const closeModal = () => {
  modalVisible.value = false;
};
</script>
