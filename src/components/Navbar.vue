<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import { RouterLink } from "vue-router";

const isMenuOpen = ref(false);
const isBlurred = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

function handleScroll() {
  isBlurred.value = window.scrollY > 0;
}

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <nav :class="{ blurred: isBlurred }" class="navbar sticky top-0 bg-transparent z-50">
    <div class="max-w-4xl xl:max-w-5xl mx-auto px-5 py-2.5 lg:py-4 flex items-center justify-between">
      <button>
        <div class="flex items-center space-x-2">
          <h2 class="text-black dark:text-white font-bold text-2xl">MyPorto</h2>
        </div>
      </button>
      <div class="hidden lg:flex space-x-10 text-base font-bold text-black/60 dark:text-white">
        <RouterLink to="/" active-class="active" class="hover:underline hover:underline-offset-4 hover:w-fit transition-all duration-100 ease-linear">Home</RouterLink>
        <a href="#" class="hover:underline hover:underline-offset-4 hover:w-fit transition-all duration-100 ease-linear">About Me</a>
        <a href="#" class="hover:underline hover:underline-offset-4 hover:w-fit transition-all duration-100 ease-linear">Project</a>
        <a href="#" class="hover:underline hover:underline-offset-4 hover:w-fit transition-all duration-100 ease-linear">Services</a>
      </div>
      <div class="lg:hidden">
        <button @click="toggleMenu" class="text-black dark:text-white focus:outline-none">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
          </svg>
        </button>
      </div>
    </div>
    <div v-if="isMenuOpen" class="lg:hidden">
      <RouterLink to="/" active-class="active" class="block text-gray-300 hover:text-white py-2 px-4">Home</RouterLink>
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4">Our services</a>
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4">About</a>
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4">Contact</a>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  transition: background-color 0.3s ease, backdrop-filter 0.3s ease;
}

.blurred {
  backdrop-filter: blur(10px);
  background-color: rgba(255, 255, 255, 0.75); /* Transparansi untuk tema terang */
}

.dark .blurred {
  background-color: rgba(31, 41, 55, 0.75); /* Transparansi untuk tema gelap */
}

.active {
  color: black;
  font-weight: bolder;
  text-decoration: underline;
}
</style>
