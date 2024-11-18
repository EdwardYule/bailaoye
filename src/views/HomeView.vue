<script setup lang="ts">
import { ref } from 'vue'
import Logo from './test.jpg'

const touchStartY = ref(0)
const touchEndY = ref(0)
const handStyle = ref({
  transform: 'translateY(0px)',
})

function handleTouchStart(event: TouchEvent) {
  touchStartY.value = event.touches[0].clientY
}

function handleTouchMove(event: TouchEvent) {
  touchEndY.value = event.touches[0].clientY
  const deltaY = touchEndY.value - touchStartY.value
  handStyle.value = {
    transform: `translate(-50%, ${deltaY}px)`,
  }
}

</script>

<template>
  <main @touchstart="handleTouchStart" @touchmove="handleTouchMove">
    <div class="hand" :style="handStyle">
      <img :src="Logo" alt="Hand" />
    </div>
  </main>
</template>

<style scoped lang="less">
.hand {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>

