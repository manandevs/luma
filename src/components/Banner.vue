<script setup lang="ts">
import Logo from './Logo.vue';
const rows = ['Shine. Grow. Scale.', 'Grow. Scale. Shine.', 'Scale. Shine. Grow.'];
</script>

<template>
  <section class="px-5 md:px-12 lg:px-20">
    <div class="relative bg-luma overflow-hidden py-6 lg:py-8">
      <!-- Hollow marquee text -->
      <div class="flex flex-col gap-2 select-none" aria-hidden="true">
        <div v-for="(row, i) in rows" :key="i" class="flex w-max"
          :class="i % 2 ? 'animate-marquee-reverse' : 'animate-marquee'">
          <span v-for="n in 4" :key="n"
            class="h-display text-[56px] md:text-[96px] lg:text-[120px] leading-none pr-8 whitespace-nowrap text-outline-black">
            {{ row }}
          </span>
        </div>
      </div>

      <!-- Black band -->
      <div class="relative mt-6 mx-4 md:mt-0 md:absolute md:inset-x-0 md:top-1/2 md:-translate-y-1/2 lg:mx-16 bg-black grid md:grid-cols-[auto_1fr]">
        <div class="flex flex-col gap-4 p-6 lg:p-8 border-b md:border-b-0 md:border-r border-white/15 md:max-w-[300px]">
          <Logo mark-only class="[&_svg]:w-12 [&_svg]:h-12" />
          <p class="text-xs lg:text-sm text-white/70 leading-relaxed">
            Luma helps businesses around the world grow online, pairing the best marketing talent with data that
            proves every decision.
          </p>
        </div>
        <div class="p-6 lg:p-8 flex items-center">
          <p class="text-sm lg:text-base leading-relaxed max-w-lg">
            For founders and marketing teams, Luma strives for more. More reach. More leads. More revenue.
            <span class="font-semibold text-gradient">By finding your next growth channel</span>, we make your
            marketing work as hard as you do.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
