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
  <nav
    :class="{ blurred: isBlurred }"
    class="navbar bg-gray-800 p-4 shadow-lg max-w-3xl w-full mx-auto rounded-lg -mt-16"
  >
    <div class="container mx-auto flex items-center">
      <div class="text-white text-2xl font-bold">MyPorto</div>
      <div class="hidden md:flex space-x-4 ml-auto">
        <RouterLink active-class="active" class="text-gray-300 hover:text-white" to="/">Home</RouterLink>
        <a href="#" class="text-gray-300 hover:text-white">About</a>
        <a href="#" class="text-gray-300 hover:text-white">Project</a>
        <a href="#" class="text-gray-300 hover:text-white">Experience</a>
      </div>
      <div class="md:hidden">
        <button
          @click="toggleMenu"
          class="text-gray-300 hover:text-white focus:outline-none"
        >
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16m-7 6h7"
            ></path>
          </svg>
        </button>
      </div>
    </div>
    <div v-if="isMenuOpen" class="md:hidden">
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4"
        >Home</a
      >
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4"
        >About</a
      >
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4"
        >Project</a
      >
      <a href="#" class="block text-gray-300 hover:text-white py-2 px-4"
        >Experience</a
      >
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: sticky;
  top: 20px; /* memberikan sedikit jarak dari atas */
  z-index: 10;
  transition: background-color 0.3s ease, backdrop-filter 0.3s ease;
  border-radius: 15px; /* sudut melengkung */
  box-shadow: 0 10px 14px rgba(0, 0, 0, 0.1); /* bayangan untuk efek 3D */
}

.blurred {
  backdrop-filter: blur(10px);
  background-color: rgba(31, 41, 55, 0.75); /* Menambahkan transparansi */
}

.container {
  display: flex;
  justify-content: center; /* Menempatkan konten di tengah */
}

nav a {
  transition: color 0.3s ease;
}

.active {
  font-weight: bold;
  text-decoration: underline;
}
</style>
