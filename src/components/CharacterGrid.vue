<template>
  <section class="grid-section">
    <h2>best girls</h2>
    <div class="grid">
      <div 
        v-for="(char, i) in chars" 
        :key="i" 
        class="card"
        ref="cards"
      >
        <div class="card-img" :style="{ backgroundImage: `url(${char.img})` }"></div>
        <div class="info">
          <h3>{{ char.name }}</h3>
          <p>{{ char.role }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const cards = ref([]);

const chars = [
  { name: 'REI', img: 'https://i.pinimg.com/736x/fc/59/7e/fc597e42f8f4bdd41d927778630d7b9d.jpg' },
  { name: 'CC', img: 'https://i.pinimg.com/736x/bf/27/9c/bf279c31e82bc6beb99e691014354e1b.jpg' },
  { name: 'MISA', img: 'https://i.pinimg.com/736x/c5/25/ae/c525ae07a8ec22bef54ee0dadeaa39d6.jpg' },
];

onMounted(() => {
  // Анимация появления карточек по очереди (Stagger)
  gsap.from(cards.value, {
    scrollTrigger: {
      trigger: ".grid-section",
      start: "top 70%",
    },
    y: 100,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2, // Задержка между элементами
    ease: "power2.out"
  });
});
</script>

<style lang="scss" scoped>
.grid-section {
  padding: 100px 20px;
  background: linear-gradient(180deg, var(--bg) 0%, #1a1a2e 100%);
  text-align: center;
}

h2 { font-size: 3rem; margin-bottom: 60px; }

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto;
}

.card {
  background: rgba(255,255,255,0.05);
  border-radius: 15px;
  overflow: hidden;
  border: 1px solid rgba(255,255,255,0.1);
  transition: transform 0.3s ease, border-color 0.3s;
  cursor: pointer;

  &:hover {
    transform: translateY(-10px);
    border-color: var(--primary);
    
    .card-img { transform: scale(1.1); }
  }
}

.card-img {
  height: 350px;
  background-size: cover;
  background-position: center;
  transition: transform 0.5s ease;
}

.info { padding: 20px; }
h3 { color: var(--accent); margin-bottom: 5px; }
</style>