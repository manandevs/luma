<script setup lang="ts">
import WaveMesh from './WaveMesh.vue';

const socials = [
  {
    name: 'LinkedIn',
    path: 'M4.98 3.5a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5zM3 9h4v12H3zM9 9h3.8v1.7h.05c.53-1 1.83-2.05 3.77-2.05C20.6 8.65 21 11.3 21 14.7V21h-4v-5.6c0-1.34-.03-3.06-1.86-3.06-1.87 0-2.15 1.46-2.15 2.96V21H9z',
  },
  {
    name: 'Instagram',
    path: 'M12 7.3a4.7 4.7 0 1 0 0 9.4 4.7 4.7 0 0 0 0-9.4zm0 7.7a3 3 0 1 1 0-6 3 3 0 0 1 0 6zm4.9-8.95a1.1 1.1 0 1 1-2.2 0 1.1 1.1 0 0 1 2.2 0zM12 3.6c2.7 0 3.05 0 4.1.06 2.75.12 4.03 1.43 4.15 4.15.05 1.06.06 1.38.06 4.08s0 3.05-.06 4.1c-.12 2.72-1.4 4.03-4.15 4.15-1.06.05-1.38.06-4.1.06s-3.04 0-4.1-.06c-2.76-.12-4.03-1.44-4.15-4.15-.05-1.06-.06-1.38-.06-4.1s0-3.03.06-4.08C3.87 5.08 5.15 3.78 7.9 3.66 8.96 3.61 9.28 3.6 12 3.6z',
  },
  {
    name: 'X',
    path: 'M17.75 3h3.07l-6.7 7.66L22 21h-6.17l-4.83-6.32L5.47 21H2.4l7.17-8.2L2 3h6.33l4.37 5.77zm-1.08 16.18h1.7L7.4 4.73H5.58z',
  },
];
</script>

<template>
  <footer class="relative pt-16">
    <div class="px-5 md:px-12 lg:px-20 flex flex-col md:flex-row md:items-end justify-between gap-8">
      <div>
        <a href="#" class="font-display text-2xl font-bold tracking-tight lowercase">luma<span class="text-neon">.</span></a>
        <div class="mt-4 flex flex-wrap items-center gap-x-6 gap-y-2 text-xs text-white/60">
          <span>&copy; {{ new Date().getFullYear() }} Luma. All rights reserved.</span>
          <a href="#" class="hover:text-white underline-offset-4 hover:underline">Privacy Policy</a>
        </div>
      </div>

      <div class="flex items-center gap-3">
        <a v-for="s in socials" :key="s.name" href="#" :aria-label="s.name"
          class="w-9 h-9 rounded-full bg-luma flex items-center justify-center text-black hover:scale-110 transition-transform">
          <svg viewBox="0 0 24 24" class="w-4 h-4" fill="currentColor" aria-hidden="true"><path :d="s.path" /></svg>
        </a>
      </div>
    </div>

    <p class="px-5 md:px-12 lg:px-20 mt-8 label text-white/40">Powered by Suggui</p>

    <WaveMesh class="mt-6" :height="220" :lines="30" gradient :seed="2" />
  </footer>
</template>
