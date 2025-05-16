<script setup>
const rings = [
  { top: "5%", side: "left", offset: "0" },
  { top: "25%", side: "right", offset: "0" },
  { top: "45%", side: "left", offset: "0" },
  { top: "65%", side: "right", offset: "0" },
  { top: "85%", side: "left", offset: "0" },
];
</script>

<template>
  <div class="rings-container">
    <div
      v-for="(ring, i) in rings"
      :key="i"
      class="ring"
      :class="ring.side"
      :style="{ top: ring.top, [ring.side]: ring.offset }"
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
