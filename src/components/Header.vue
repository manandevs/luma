<script setup>
import { ref } from 'vue';

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};
</script>

<template>
  <nav
    class="sticky top-0 z-50 w-full px-5 py-5 md:px-[100px] flex items-center justify-between backdrop-blur-xl">
    <!-- Brand -->
    <a href="#" class="flex items-center">
      <!-- <svg width="36" height="36" viewBox="0 0 36 36" fill="#000" xmlns="http://www.w3.org/2000/svg"
        class="w-6 h-6 lg:w-9 lg:h-9">
        <path
          d="M17.999 5.535l17.6-5.186L30.465 18 35.6 35.601l-17.601-5.136L.348 35.602l5.185-17.6L.348.348l17.65 5.186z" />
      </svg> -->
      <img src="/images/logo.png" alt="Luma Logo" class="w-6 h-6 lg:w-12 lg:h-12 drop-shadow-[0_0_30px_#008000]" />
      <span class="text-xl lg:text-2xl font-semibold">
        Luma
      </span>
    </a>

    <div class="max-w-md flex items-center justify-center gap-5">
      <a href="https://suggui.vercel.app/" class="block w-full text-center py-2 px-3 bg-white rounded-[14px] text-black" @click="closeMenu">
        Request a quote
      </a>

      <button class="p-2" @click="toggleMenu">
        <svg width="26" height="19" viewBox="0 0 26 19" fill="none" stroke="#fff" xmlns="http://www.w3.org/2000/svg">
          <path d="M1 1.80664H25" stroke-width="2" stroke-linecap="round" />
          <path d="M1 9.80664H25" stroke-width="2" stroke-linecap="round" />
          <path d="M1 17.8066H25" stroke-width="2" stroke-linecap="round" />
        </svg>
      </button>
    </div>
  </nav>
</template>