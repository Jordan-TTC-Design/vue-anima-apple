<script setup>
import { computed, onMounted, ref } from 'vue';
const progress = ref(0);
const fixClass = computed(() => {
  return progress.value > 1;
});
onMounted(() => {
  const app = document.querySelector('#app');
  app.addEventListener('scroll', () => {
    if (app.scrollTop < window.innerHeight) {
      progress.value = 3;
    } else if (app.scrollTop > window.innerHeight * 2) {
      progress.value = 1;
    } else {
      progress.value =
        3 - 2 * ((app.scrollTop - window.innerHeight) / window.innerHeight);
    }
  });
});
</script>

<template>
  <!-- 需要高度撐出捲軸高度 -->
  <div class="section section--text">
    <h2>這台相機，最懂拍出你的型</h2>
  </div>
  <div
    id="section2"
    class="section"
    :style="{ '--scale': progress }"
    :class="{ 'section--sticky': fixClass }"
  >
    <div class="phone">
      <img src="https://picsum.photos/id/237/1920/1200" alt="主圖" />
      <div class="rect"></div>
    </div>
  </div>
  <div id="section3" class="section" :class="{ 'section--static': fixClass }">
    <div class="phone">
      <img src="https://picsum.photos/id/237/1920/1200" alt="主圖" />
      <div class="rect"></div>
    </div>
  </div>
  <div class="section section--text">
    <h2>這台相機，最懂拍出你的型</h2>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  overflow: hidden;
}
#app {
  width: 100vw;
  height: 100vh;
  overflow: auto;
}
.section {
  position: relative;
  width: 100%;
  height: 100%;
  background-color: #fff;
  overflow: hidden;
}
.section--text {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 64px;
}
#section2,
#section3 {
  background-color: #e2e2e2;
}
#section2 {
  --scale: 3;
}
#section3 {
  --scale: 1;
}
.section--sticky {
  position: sticky;
  top: 0;
  left: 0;
}
.section--static {
  position: static;
}
.phone {
  position: absolute;
  width: 100%;
  height: 100%;
  transform: scale(var(--scale));
}
.phone > * {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.phone > img {
  clip-path: inset(16% 8% round 1%);
  width: 60%;
  height: auto;
}
.phone > .rect {
  border: 8px solid white;
  width: 50%;
  height: 0;
  padding-top: 25%;
  border-radius: 0.5rem;
}
</style>
