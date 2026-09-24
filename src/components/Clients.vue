<script setup lang="ts">
const logos = [
  { name: 'Amazon', src: '/images/company-amazon.webp' },
  { name: 'Dribbble', src: '/images/company-dribbble.webp' },
  { name: 'HubSpot', src: '/images/company-hubspot.webp' },
  { name: 'Notion', src: '/images/company-notion.webp' },
  { name: 'Netflix', src: '/images/company-netflix.webp' },
  { name: 'Zoom', src: '/images/company-zoom.webp' },
];
</script>

<template>
  <section id="clients" class="px-5 md:px-12 lg:px-20 py-16 lg:py-24 scroll-mt-24">
    <p class="label text-center text-white/50">Trusted by teams at</p>
    <div class="mt-10 mx-auto max-w-4xl grid grid-cols-2 sm:grid-cols-3 gap-4 lg:gap-5">
      <div v-for="logo in logos" :key="logo.name"
        class="aspect-[16/10] border border-line flex items-center justify-center p-6 lg:p-10 hover:border-white/50 transition-colors">
        <img :src="logo.src" :alt="logo.name" class="max-h-10 lg:max-h-12 w-auto brightness-0 invert opacity-90" />
      </div>
    </div>
  </section>
</template>
