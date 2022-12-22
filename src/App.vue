<template>
  <theHeader />
  <GoogleMap
    ref="mapRef"
    :api-key="apiKey"
    style="width: 100%; height: 700px"
    :center="center"
    :zoom="zoomLevel"
    @dragend="dragMap"
    @zoom_changed="changeZoom"
  >
    <CustomControl position="TOP_CENTER">
      <button class="custom-btn" @click="centerMap()">CENTER</button>
    </CustomControl>
    <Marker
      v-for="camera in cameras"
      :options="{ position: { lat: camera.lat, lng: camera.lng } }"
      @click="
        showModal();
        getVideoSrc(camera);
      "
    ></Marker>
  </GoogleMap>
  <locationLists
    :cameras="cameras"
    @changeCenter="changeCenter"
  ></locationLists>

  <video-modal :isVisible="modalVisible" @close="closeModal">
    <YouTube
      v-if="videoSrc"
      :src="videoSrc"
      @ready="onReady"
      @playback-quality-change="setVolumeZero"
      ref="youtube"
      host="https://www.youtube-nocookie.com"
    />
  </video-modal>
</template>

<script setup>
import { ref } from "vue";
import { GoogleMap, Marker, CustomControl } from "vue3-google-map";
import YouTube from "vue3-youtube";
import { liveCameras } from "./live-cameras";
import videoModal from "./components/videoModal.vue";
import theHeader from "./components/theHeader.vue";
import locationLists from "./components/locationLists.vue";

const apiKey = import.meta.env.VITE_GOOGLE_MAP_API_KEY;
const youtube = ref(null);
const onReady = () => {
  youtube._rawValue.playVideo();
};
const setVolumeZero = () => {
  youtube._rawValue.setVolume(0);
};
const cameras = liveCameras;

let zoomLevel = ref(2);
let center = ref({ lat: 36.0, lng: 180.0 });
const centerMap = () => {
  center.value = { lat: 36.0, lng: 180.0 };
  zoomLevel.value = 2;
};
const changeCenter = (lat, lng) => {
  center.value = { lat: lat, lng: lng };
};
const mapRef = ref(null);
const dragMap = () => {
  center.value = {
    lat: mapRef.value.map.center.lat(),
    lng: mapRef.value.map.center.lng(),
  };
};
const changeZoom = () => {
  zoomLevel.value = mapRef.value.map.getZoom();
};

let modalVisible = ref(false);
const showModal = () => {
  modalVisible.value = true;
};
const closeModal = () => {
  modalVisible.value = false;
};

let videoSrc = ref("");
const getVideoSrc = (camera) => {
  videoSrc.value = camera.src;
};
</script>

<style scoped>
.custom-btn {
  box-sizing: border-box;
  background: white;
  height: 30px;
  width: auto;
  border-radius: 2px;
  border: 0px;
  margin: 10px;
  padding: 5px;
  font-size: 1.25rem;
  text-transform: none;
  appearance: none;
  cursor: pointer;
  user-select: none;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 1px 4px -1px;
  overflow: hidden;
}
</style>
