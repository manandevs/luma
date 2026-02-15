<script setup>
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
  <section class="mt-[60px] lg:mt-[70px] w-full overflow-hidden bg-[#008000] py-5">

    <div class="flex w-max items-center gap-9 lg:gap-24">

      <div class="flex gap-9 lg:gap-24 items-center shrink-0 animate-marquee">
        <img v-for="logo in logos" :key="logo.name" :src="logo.src" :alt="logo.name"
          class="h-8 md:h-12 w-auto cursor-pointer brightness-0" />
      </div>
      <div class="flex gap-9 lg:gap-24 items-center shrink-0 animate-marquee" aria-hidden="true">
        <img v-for="logo in logos" :key="`${logo.name}-duplicate`" :src="logo.src" :alt="logo.name"
          class="h-8 md:h-12 w-auto cursor-pointer brightness-0" />
      </div>

    </div>
  </section>
</template>

<style scoped>
.animate-marquee {
  animation: marquee 25s linear infinite;
}

@keyframes marquee {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(-50%);
  }
}
</style>