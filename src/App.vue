<script setup lang="ts">
import { RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
</script>

<template>
  <header class="fixed top-0 left-0 right-0 z-50 w-full">
    <NavBar />
  </header>

  <main class="flex items-center justify-center min-h-screen">
    <RouterView class="views"/>
  </main>

</template>

<style scoped>
  .min-h-screen {
    min-height: 100vh;
  }

  .views {
    width: 98vw;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 5rem;
    padding-top: 4rem;
  }

  @media (min-width: 1024px) {
    .views {
      min-height: 100vh;
      display: flex;
      align-items: center;
    }
  }
</style>

