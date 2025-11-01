<script setup lang="ts">
import { ref, onMounted } from 'vue';

const chuseokMessage = ref('풍요로운 결실 맺으시길 바랍니다.');
// 요청에 따라 제목을 배열로 분리하여 줄바꿈 처리
const titleLines = ref(['🌕 즐거운', '한가위 🌕']);

const isMounted = ref(false);

onMounted(() => {
  setTimeout(() => {
    isMounted.value = true;
  }, 100);
});
</script>

<template>
  <div class="h-screen w-full bg-black text-white flex flex-col items-center justify-center overflow-hidden relative font-inter p-4">
    <div class="starfield"></div>
    <div class="shooting-star"></div>

    <div
        class="moon-container"
        :class="{ 'animate-moon': isMounted }"
        aria-label="보름달"
    >
      <div class="moon shadow-2xl">
        <div class="text-center p-8 transition-opacity duration-1000" :class="{ 'opacity-100': isMounted, 'opacity-0': !isMounted }">
          <h1 class="text-5xl sm:text-6xl font-extrabold mb-6 text-yellow-300 drop-shadow-lg leading-tight">
            <div v-for="(line, index) in titleLines" :key="index">{{ line }}</div>
          </h1>
          <p class="text-2xl sm:text-3xl font-light text-gray-200 mt-4">
            {{ chuseokMessage }}
          </p>
          <div class="mt-8 text-lg text-gray-400">
            <p>온 가족이 함께하는 행복한 명절 보내세요.</p>
          </div>
        </div>
      </div>
    </div>

    <footer class="absolute bottom-6 text-sm sm:text-base text-gray-500 z-20">
      &copy; 2024 Han-gawi Night
    </footer>
  </div>
</template>

<style scoped>
.starfield {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: transparent;
  z-index: 1;
  box-shadow:
      0 0 1px 1px #fff, -100vw 50vh 2px 2px #fff, -50vw -10vh 1px 1px #fff, 10vw 80vh 2px 2px #fff, -80vw 20vh 1px 1px #fff, 20vw -70vh 1px 1px #fff,
      40vw 30vh 3px 3px #f7f3e8, -60vw -40vh 2px 2px #f7f3e8, 70vw 60vh 3px 3px #f7f3e8, -30vw 90vh 2px 2px #f7f3e8;
  animation: twinkle 30s infinite alternate;
}

.shooting-star {
  position: absolute;
  top: 0;
  left: 50%;
  width: 10px;
  height: 2px;
  background: linear-gradient(90deg, #ffffff, transparent);
  transform: rotate(45deg);
  z-index: 5;
  animation: shoot 5s infinite;
  opacity: 0;
}

@keyframes shoot {
  0% { transform: translate(100vw, -10vh) rotate(45deg); opacity: 0; }
  2% { opacity: 1; }
  10% { transform: translate(-50vw, 50vh) rotate(45deg); opacity: 1; }
  12% { opacity: 0; }
  100% { opacity: 0; }
}

@keyframes twinkle {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.8; }
}

.moon-container {
  position: relative;
  z-index: 10;
  transition: transform 1s ease-out, opacity 1s ease-out;
  opacity: 0;
  transform: scale(0.8) translateY(50px);
}

.animate-moon {
  opacity: 1;
  transform: scale(1) translateY(0);
}

.moon {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle at 75% 30%, #fefefe 0%, #ffe9a6 60%, #ffc04d 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 100px rgba(255, 255, 150, 0.9),
  0 0 250px rgba(255, 180, 0, 0.6);
  animation: pulse 4s infinite alternate;
}

@keyframes pulse {
  0% { transform: scale(1); box-shadow: 0 0 100px rgba(255, 255, 150, 0.9), 0 0 250px rgba(255, 180, 0, 0.6); }
  100% { transform: scale(1.02); box-shadow: 0 0 110px rgba(255, 255, 150, 1), 0 0 270px rgba(255, 180, 0, 0.7); }
}

@media (max-width: 640px) {
  .moon {
    width: 280px;
    height: 280px;
  }
}
</style>