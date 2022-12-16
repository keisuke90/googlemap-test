<script setup lang="ts">
interface Props {
  isVisible: boolean;
}
interface Emits {
  (event: "close"): void;
}
defineProps<Props>();
const emit = defineEmits<Emits>();
const close = (): void => {
  emit("close");
};
</script>

<template>
  <teleport to="body">
    <div
      class="modal"
      id="sample-modal"
      v-show="isVisible"
      @click="close"
    ></div>
    <div class="modal-content" v-show="isVisible"><slot /></div>
  </teleport>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.modal-content {
  position: fixed;
  top: 30%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: auto;
  height: auto;
  border-radius: 20px;
}
</style>
