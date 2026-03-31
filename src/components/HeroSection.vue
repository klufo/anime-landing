<template>
  <section class="hero">
    <div class="hero-bg" ref="bgRef"></div>
    <div class="content">
      <h1 class="title" ref="titleRef">refraindre  <span class="highlight">stak</span></h1>
      <p class="subtitle" ref="subRef">the best past.</p>
      <button class="btn" ref="btnRef">СМОТРЕТЬ ТРЕЙЛЕР</button>
    </div>
    
    <!-- Персонаж 1: Слева (голубая подсветка) -->
    <img src="@/assets/char2.png" alt="Hero Left" class="character character-left glow-cyan" ref="charRef1">
    
    <!-- Персонаж 2: По центру (зелёная подсветка) -->
    <img src="@/assets/char3.png" alt="Hero Center" class="character character-center glow-green" ref="charRef2">
    
    <!-- Персонаж 3: Справа (красная подсветка) -->
    <img src="@/assets/char.png" alt="Hero Right" class="character character-right glow-red" ref="charRef3">
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const bgRef = ref(null);
const titleRef = ref(null);
const subRef = ref(null);
const btnRef = ref(null);
const charRef1 = ref(null);
const charRef2 = ref(null);
const charRef3 = ref(null);

onMounted(() => {
  const tl = gsap.timeline();
  tl.from(titleRef.value, { y: 100, opacity: 0, duration: 1, ease: "power4.out" })
    .from(subRef.value, { y: 50, opacity: 0, duration: 0.8 }, "-=0.5")
    .from(charRef1.value, { x: -150, opacity: 0, duration: 1, ease: "power3.out" }, "-=0.8")
    .from(charRef2.value, { y: 100, opacity: 0, duration: 1, ease: "power3.out" }, "-=0.9")
    .from(charRef3.value, { x: 150, opacity: 0, duration: 1, ease: "power3.out" }, "-=0.9")
    .from(btnRef.value, { scale: 0, duration: 0.5, ease: "back.out(1.7)" }, "-=0.5");

  gsap.to(bgRef.value, {
    yPercent: 30,
    ease: "none",
    scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: true }
  });

  gsap.to(charRef1.value, { yPercent: -8, xPercent: -3, ease: "none", scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: true }});
  gsap.to(charRef2.value, { yPercent: -12, ease: "none", scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: true }});
  gsap.to(charRef3.value, { yPercent: -8, xPercent: 3, ease: "none", scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: true }});

  // Анимация парения (лебитации)
  gsap.to(charRef1.value, { y: -5, duration: 2, repeat: -1, yoyo: true, ease: "sine.inOut" });
  gsap.to(charRef2.value, { y: -5, duration: 3, repeat: -1, yoyo: true, ease: "sine.inOut", delay: 0.5 });
  gsap.to(charRef3.value, { y: -5, duration: 2.2, repeat: -1, yoyo: true, ease: "sine.inOut" });
});
</script>

<style lang="scss" scoped>
// 🎨 НАСТРОЙКИ ЦВЕТОВ ПОДСВЕТКИ
$glow-red:    #ff0055;
$glow-cyan:   #00e5ff;
$glow-green:  #00ff88;
$glow-blur-1: 4px;
$glow-blur-2: 15px;
$glow-blur-3: 40px;

.hero {
  height: 100vh;
  width: 100%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 120%;
  background: url('@/assets/bg.jpg') no-repeat center/cover;
  z-index: 1;
  filter: brightness(0.5);
}

.content {
  position: relative;
  z-index: 10;
  text-align: center;
  pointer-events: none;
}

.title {
  font-size: 5rem;
  text-shadow: 0 0 20px var(--primary);
}

.highlight { color: var(--primary); }

.btn {
  pointer-events: auto;
  margin-top: 20px;
  padding: 15px 40px;
  background: transparent;
  border: 2px solid var(--accent);
  color: var(--accent);
  font-family: 'Orbitron';
  font-size: 1.2rem;
  cursor: pointer;
  transition: 0.3s;

  &:hover {
    background: var(--accent);
    color: var(--bg);
    box-shadow: 0 0 30px var(--accent);
  }
}

/* 🔷 Базовые стили для всех персонажей */
.character {
  position: absolute;
  bottom: 0;
  height: 85vh;
  z-index: 5;
  pointer-events: none;
  will-change: filter, transform;
  transition: filter 0.3s ease;
}

/* 📍 ПОЗИЦИОНИРОВАНИЕ - БАЗОВЫЕ ЗНАЧЕНИЯ (для 3440x1440 и шире) */
.character-left {
  left: 8%;
  z-index: 4;
}

.character-center {
  left: 50%;
  transform: translateX(-50%);
  height: 95vh;
  z-index: 6;
}

.character-right {
  right: 8%;
  z-index: 4;
}

/* 🌈 СИСТЕМА ПОДСВЕТКИ СИЛУЭТА */
.glow-red {
  filter: 
    drop-shadow(0 0 2px $glow-red)
    drop-shadow(0 0 $glow-blur-1 $glow-red)
    drop-shadow(0 0 $glow-blur-2 $glow-red)
    drop-shadow(0 0 $glow-blur-3 rgba($glow-red, 0.4));
}

.glow-cyan {
  filter: 
    drop-shadow(0 0 2px $glow-cyan)
    drop-shadow(0 0 $glow-blur-1 $glow-cyan)
    drop-shadow(0 0 $glow-blur-2 $glow-cyan)
    drop-shadow(0 0 $glow-blur-3 rgba($glow-cyan, 0.4));
}

.glow-green {
  filter: 
    drop-shadow(0 0 2px $glow-green)
    drop-shadow(0 0 $glow-blur-1 $glow-green)
    drop-shadow(0 0 $glow-blur-2 $glow-green)
    drop-shadow(0 0 $glow-blur-3 rgba($glow-green, 0.4));
}

/* ✨ Эффект усиления при наведении */
.character:hover {
  filter: 
    drop-shadow(0 0 4px currentColor)
    drop-shadow(0 0 20px currentColor)
    drop-shadow(0 0 50px currentColor);
}

/* ======================================== */
/* 📱 АДАПТАЦИЯ ПОД РАЗРЕШЕНИЯ ЭКРАНА */
/* ======================================== */

/* 2K и стандартные широкие экраны (2560px - 1921px) */
@media (max-width: 2560px) {
  .character { height: 80vh; }
  .character-center { height: 90vh; }
  .character-left { left: 5%; }
  .character-right { right: 5%; }
}

/* Full HD (1920x1080) - ГЛАВНОЕ ИСПРАВЛЕНИЕ */
@media (max-width: 1920px) {
  .character { 
    height: 75vh;  /* Уменьшаем высоту, чтобы не занимали весь экран */
    bottom: -30px; /* Чуть опускаем вниз */
  }
  
  .character-center { 
    height: 85vh;  /* Центральный всё ещё крупнее */
    bottom: 0;
  }
  
  /* Разводим персонажей дальше по краям */
  .character-left { 
    left: 2%; 
  }
  
  .character-right { 
    right: 2%; 
  }
}

/* Ноутбуки 15-16 дюймов (1600px - 1366px) */
@media (max-width: 1600px) {
  .character { height: 70vh; }
  .character-center { height: 80vh; }
  .character-left { left: 0%; }
  .character-right { right: 0%; }
}

/* Планшеты и маленькие ноутбуки (1365px - 1025px) */
@media (max-width: 1365px) {
  .character { 
    height: 60vh;
    bottom: -50px;
  }
  .character-center { 
    height: 70vh;
  }
  .character-left { 
    left: -5%;  /* Чуть выпускаем за экран */
    opacity: 0.8;
  }
  .character-right { 
    right: -5%;
    opacity: 0.8;
  }
}

/* Планшеты вертикальные (1024px и меньше) */
@media (max-width: 1024px) {
  .title { font-size: 3.5rem; }
  
  .character { 
    height: 50vh;
    bottom: -80px;
  }
  .character-center { 
    height: 60vh;
  }
  .character-left { 
    left: -10%;
    opacity: 0.6;
  }
  .character-right { 
    right: -10%;
    opacity: 0.6;
  }
}

/* Мобильные устройства (768px и меньше) */
@media (max-width: 768px) {
  .title { font-size: 2.5rem; }
  .subtitle { font-size: 1rem; }
  
  /* На мобильных оставляем только центрального персонажа */
  .character-left,
  .character-right {
    display: none;
  }
  
  .character-center {
    height: 55vh;
    left: 50%;
    bottom: -50px;
  }
}

/* Очень маленькие экраны (480px и меньше) */
@media (max-width: 480px) {
  .title { font-size: 2rem; }
  
  .character-center {
    height: 45vh;
    bottom: -30px;
  }
}
</style>