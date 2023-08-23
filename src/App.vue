<script setup>
import Header from './components/Header.vue';
import Menu from './components/Menu.vue';
import Pokemons from './components/Pokemons.vue';
</script>

<template>
  <header style="display: flex; align-items: center; justify-content: space-between;">
    <Header />
    <Menu />
  </header>
  <main>
    <!-- <TheWelcome /> -->
    <Pokemons />
  </main>
</template>

<style scoped>

</style>
