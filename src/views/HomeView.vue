<script setup>
import { ref } from 'vue'
import banner from '../components/banner/BannerHome.vue'
</script>

<template>
  <banner />
  <div class="max-w-screen-xl mx-auto p-5 sm:p-10 md:p-16">
    <div class="grid grid-cols-1 md:grid-cols-3 sm:grid-cols-2 gap-7">
      <div
        v-for="imageUrl in imagesFromLocalStorage"
        :key="imageUrl"
        class="rounded overflow-hidden shadow-lg"
      >
        <a href="#"></a>
        <div class="relative">
          <a href="#">
            <img class="object-cover h-48 w-full" :src="imageUrl" alt="Sunset in the mountains" />
            <div
              class="hover:bg-transparent transition duration-300 absolute bottom-0 top-0 right-0 left-0 bg-gray-900 opacity-25"
            ></div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'

const imagesFromLocalStorage = ref(JSON.parse(localStorage.getItem('uploadImages')) || [])

export { imagesFromLocalStorage }
</script>
