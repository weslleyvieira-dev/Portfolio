<script setup>
const rings = [
  { top: "5%", side: "left"},
  { top: "30%", side: "right"},
  { top: "50%", side: "left"},
  { top: "70%", side: "right"},
  { top: "90%", side: "left"},
];
</script>

<template>
  <div class="rings-container">
    <div
      v-for="(ring, i) in rings"
      :key="i"
      class="ring"
      :class="ring.side"
      :style="{ top: ring.top, [ring.side]: 0 }"
    />
  </div>
</template>

<style scoped>
.rings-container {
  position: absolute;
  inset: 0;
  overflow-x: hidden;
  pointer-events: none;
}

.ring {
  position: absolute;
  width: 33.125rem;
  height: 8.125rem;
  background-image: url("/assets/images/pattern-rings.svg");
  background-repeat: no-repeat;
  background-size: contain;
}

.ring.left {
  transform: translateX(-50%);
}

.ring.right {
  transform: translateX(50%);
}
</style>
