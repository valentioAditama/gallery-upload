<script setup>
import banner from '../components/banner/BannerHome.vue'
</script>

<template>
  <banner />
  <div class="max-w-screen-xl mx-auto p-5 sm:p-10 md:p-16">
    <div class="grid grid-cols-1 md:grid-cols-3 sm:grid-cols-2 gap-7">
      <div class="rounded overflow-hidden shadow-lg">
        <a href="#"></a>
        <div class="relative">
          <a href="#">
            <img
              class="w-full"
              src="https://images.pexels.com/photos/196667/pexels-photo-196667.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=1&amp;w=500"
              alt="Sunset in the mountains"
            />
            <div
              class="hover:bg-transparent transition duration-300 absolute bottom-0 top-0 right-0 left-0 bg-gray-900 opacity-25"
            ></div>
          </a>
        </div>
      </div>
      <div class="rounded overflow-hidden shadow-lg">
        <a href="#"></a>
        <div class="relative">
          <a href="#">
            <img
              class="w-full"
              src="https://images.pexels.com/photos/196667/pexels-photo-196667.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=1&amp;w=500"
              alt="Sunset in the mountains"
            />
            <div
              class="hover:bg-transparent transition duration-300 absolute bottom-0 top-0 right-0 left-0 bg-gray-900 opacity-25"
            ></div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
