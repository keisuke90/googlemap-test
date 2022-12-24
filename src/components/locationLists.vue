<template>
  <ul class="location-wrap">
    <li class="location" @click="tagClick(camera)" v-for="camera in cameras">
      {{ camera.location }}
    </li>
  </ul>
</template>

<script setup>
const props = defineProps({
  cameras: Array,
});
const emit = defineEmits();
const tagClick = (camera) => {
  emit("changeCenter", camera.lat, camera.lng);
};
</script>

<style scoped>
.location-wrap {
  height: auto;
  padding: 20px 10px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  background-color: RGB(138, 180, 248);
}
.location {
  display: flex;
  align-items: center;
  font-weight: bold;
  list-style: none;
  color: white;
  padding: 10px;
  margin: 5px;
  cursor: pointer;
  height: 50px;
  border-radius: 24px;
  background: #8ab4f8;
  box-shadow: -5px 5px 10px #7194cb, 5px -5px 10px #a3d4ff;
}
.location:active {
  box-shadow: inset -5px 5px 10px #7194cb, inset 5px -5px 10px #a3d4ff;
}
</style>
