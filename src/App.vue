<template>
  <div class="app">
    <nav class="navbar">
      <div class="logo">refraindre<span>stak</span></div>
    </nav>
    
    <HeroSection />
    <CharacterGrid />
    
    <footer>© 2026 klufo Project</footer>
  </div>
</template>

<script setup>
import HeroSection from './components/HeroSection.vue';
import CharacterGrid from './components/CharacterGrid.vue';
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  top: 0; width: 100%;
  padding: 20px 50px;
  display: flex; justify-content: space-between;
  z-index: 100;
  background: rgba(10, 10, 18, 0.8);
  backdrop-filter: blur(10px);
  
  .logo { font-family: 'Orbitron'; font-size: 1.5rem; font-weight: bold; }
  .logo span { color: var(--primary); }
}

footer {
  padding: 40px; text-align: center; background: #050508; color: #666;
}
</style>