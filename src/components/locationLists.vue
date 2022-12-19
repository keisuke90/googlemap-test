<script setup>
const props = defineProps({
  cameras: Array,
});
</script>

<template>
  <ul class="location-wrap">
    <li class="location" v-for="camera in cameras">{{ camera.location }}</li>
  </ul>
</template>

<style scoped>
.location-wrap {
  height: auto;
  padding: 20px 10px;
  display: flex;
  flex-wrap: wrap;
  background-color: RGB(138, 180, 248);
}
.location {
  list-style: none;
  background-color: rgb(11, 4, 144);
  color: white;
  border-radius: 10px;
  padding: 10px;
  margin: 5px;
  cursor: pointer;
}
</style>
