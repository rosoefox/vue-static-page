<script setup lang="ts">
import { ref } from 'vue';

// 추석 관련 설명 및 카드 섹션 데이터 정의
const chuseokData = ref({
  title: '풍성한 한가위',
  subtitle: '온 가족이 함께하는 즐거운 명절',
  description: '한가위는 음력 8월 15일로, 곡식과 과일 등 햇것을 수확하여 조상께 감사드리는 한국의 대표적인 명절입니다. 오랜만에 모인 가족, 친지들과 함께 즐거운 시간을 보내세요.',
  sections: [
    {
      title: '전통 놀이 (Traditional Games)',
      // 전통 놀이를 상징하는 인라인 SVG 아이콘
      iconSvg: '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 19c-1.333-1.333-2-3-2-5s.667-3.667 2-5"/><path d="M12 5c1.333 1.333 2 3 2 5s-.667 3.667-2 5"/></svg>',
      items: [
        { name: '강강술래', desc: '밝은 보름달 아래 여러 사람이 손을 잡고 원을 그리며 춤추는 놀이.' },
        { name: '씨름', desc: '두 사람이 샅바를 잡고 힘과 기술을 겨루는 한국의 전통 레슬링.' },
        { name: '널뛰기', desc: '긴 널빤지의 양 끝에 올라 번갈아 뛰어오르는 여성들의 전통 놀이.' },
      ]
    },
    {
      title: '추석 음식 (Chuseok Food)',
      // 추석 음식을 상징하는 인라인 SVG 아이콘 (송편 모양)
      iconSvg: '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 21c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8z"/><path d="M16 11c-.5.5-.8.5-1.5 0s-2.5-1-3-1s-2.5 1-3 1s-.5 0-1.5 0"/></svg>',
      items: [
        { name: '송편', desc: '햅쌀로 빚어 솔잎과 함께 쪄내는 반달 모양의 대표 명절 음식.' },
        { name: '토란국', desc: '가을 토란을 넣어 끓인 국으로, 조상에게 감사하는 의미가 담겨 있음.' },
        { name: '삼색나물', desc: '도라지, 고사리, 시금치 등 세 가지 나물로 정성을 담아 준비함.' },
      ]
    }
  ]
});
</script>

<template>
  <div id="app" class="hangawi-app">
    <!-- 배경 반짝이 효과 -->
    <div class="star-field"></div>

    <main class="content-container">
      <!-- 보름달 섹션 -->
      <div class="moon-container">
        <!-- 달 모양 (SVG) -->
        <svg class="full-moon" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
          <circle cx="50" cy="50" r="50"/>
        </svg>
      </div>

      <!-- 메인 제목 및 설명 -->
      <header class="text-center mt-8 p-4">
        <h1 class="text-6xl font-extrabold text-yellow-300 drop-shadow-lg">{{ chuseokData.title }}</h1>
        <p class="text-2xl mt-2 text-white font-medium">{{ chuseokData.subtitle }}</p>
        <p class="chuseok-desc">{{ chuseokData.description }}</p>
      </header>

      <!-- 전통 놀이 및 음식 카드 섹션 -->
      <div class="cards-grid">
        <div v-for="section in chuseokData.sections" :key="section.title" class="card">
          <div class="card-header">
            <!-- 아이콘을 innerHTML로 바인딩 -->
            <div class="icon-wrapper" v-html="section.iconSvg"></div>
            <h2 class="card-title">{{ section.title }}</h2>
          </div>
          <ul class="item-list">
            <li v-for="item in section.items" :key="item.name" class="item">
              <span class="item-name">{{ item.name }}</span>
              <p class="item-desc">{{ item.desc }}</p>
            </li>
          </ul>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
/* CSS Reset 및 기본 스타일 */
:root {
  --color-primary: #fcd34d; /* Tailwind yellow-300 for highlights */
  --color-secondary: #0f172a; /* Slate-900 for dark background */
  --color-text-light: #f1f5f9; /* Slate-100 */
  --color-card-bg: rgba(255, 255, 255, 0.1);
  --color-moon: #fef08a; /* Yellow-200 for moon */
}

/* App 전체 컨테이너 스타일 */
.hangawi-app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: var(--color-text-light);
  font-family: 'Malgun Gothic', 'Noto Sans KR', sans-serif;
  overflow-x: hidden; /* 가로 스크롤 방지 */
  position: relative;
  background-color: var(--color-secondary);
}

/* === 별빛 배경 효과 === */
.star-field {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  /* 랜덤한 크기와 투명도의 별을 여러 겹의 배경으로 생성 */
  background:
      radial-gradient(2px 2px at 20px 30px, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(4px 4px at 90px 40px, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(3px 3px at 40px 70px, var(--color-primary), rgba(0,0,0,0)),
      radial-gradient(2px 2px at 150px 10px, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(3px 3px at 180px 90px, var(--color-primary), rgba(0,0,0,0)),
      radial-gradient(2px 2px at 250px 50px, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(4px 4px at 300px 80px, var(--color-primary), rgba(0,0,0,0)),
        /* 더 많은 별을 추가하여 밀도 높이기 */
      radial-gradient(1px 1px at 50% 10%, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(2px 2px at 70% 35%, var(--color-text-light), rgba(0,0,0,0)),
      radial-gradient(3px 3px at 85% 60%, var(--color-primary), rgba(0,0,0,0));

  background-size: 200px 200px, 300px 300px, 400px 400px, 500px 500px, 600px 600px, 700px 700px, 800px 800px, 900px 900px, 1000px 1000px, 1100px 1100px;
  animation: star-move 60s linear infinite; /* 별이 아주 느리게 움직이는 효과 */
  z-index: 0;
}

@keyframes star-move {
  from {
    background-position: 0 0, 0 0, 0 0, 0 0, 0 0, 0 0, 0 0, 0 0, 0 0, 0 0;
  }
  to {
    background-position: 200px 200px, 300px 300px, 400px 400px, 500px 500px, 600px 600px, 700px 700px, 800px 800px, 900px 900px, 1000px 1000px, 1100px 1100px;
  }
}
/* === 콘텐츠 컨테이너 === */
.content-container {
  position: relative;
  z-index: 1;
  width: 90%;
  max-width: 1200px;
  padding: 40px 0;
}

/* === 보름달 스타일 === */
.moon-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 20px;
}

.full-moon {
  width: 120px;
  height: 120px;
  fill: var(--color-moon);
  filter: drop-shadow(0 0 40px var(--color-moon)) drop-shadow(0 0 20px var(--color-moon));
  animation: moon-pulse 8s infinite alternate;
}

@keyframes moon-pulse {
  0% { transform: scale(1); opacity: 0.95; }
  100% { transform: scale(1.05); opacity: 1; }
}

/* === 제목 및 설명 스타일 === */
header h1 {
  font-size: 3rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

header p {
  margin-top: 0.5rem;
}

.chuseok-desc {
  background-color: rgba(0, 0, 0, 0.3);
  padding: 1rem 2rem;
  border-radius: 12px;
  margin: 1.5rem auto 3rem;
  max-width: 700px;
  font-size: 1.1rem;
  line-height: 1.6;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

/* === 카드 섹션 그리드 레이아웃 === */
.cards-grid {
  display: grid;
  gap: 30px;
  padding: 20px 0;
}

/* 반응형: 데스크탑에서는 2열, 모바일에서는 1열 */
@media (min-width: 768px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  header h1 {
    font-size: 4rem;
  }
}

/* === 개별 카드 스타일 === */
.card {
  background: var(--color-card-bg);
  border-radius: 16px;
  padding: 30px;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5);
}

.card-header {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  border-bottom: 2px solid rgba(255, 255, 255, 0.2);
  padding-bottom: 15px;
}

.icon-wrapper {
  color: var(--color-primary);
  width: 40px;
  height: 40px;
  margin-right: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-wrapper svg {
  width: 100%;
  height: 100%;
}

.card-title {
  font-size: 1.8rem;
  font-weight: bold;
  color: var(--color-primary);
}

/* === 항목 리스트 스타일 === */
.item-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.item {
  margin-bottom: 20px;
  padding: 15px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 8px;
}

.item-name {
  display: block;
  font-size: 1.3rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 5px;
}

.item-desc {
  font-size: 1rem;
  color: var(--color-text-light);
  line-height: 1.4;
}
</style>
