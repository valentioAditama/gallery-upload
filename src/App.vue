<script setup>
import navbar from './components/navbar/navbar.vue'
import footbar from './components/footer/footer.vue'
</script>

<template>
  <header>
    <navbar />
  </header>

  <RouterView />

  <footbar />
</template>
