<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue';
import Menu from './components/Menu.vue';
import Pokemons from './components/Pokemons.vue';
import Fruits from './components/Fruits.vue';

const routes = {
  '/': Pokemons,
  '/fruits': Fruits
};

const currentPath = ref(window.location.hash);

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
});
</script>

<template>
  <header style="display: flex; align-items: center; justify-content: space-between;">
    <Header />
    <Menu />
  </header>
  <main>
    <!-- <TheWelcome /> -->
    <component :is="currentView" />
  </main>
</template>

<style scoped>

</style>
