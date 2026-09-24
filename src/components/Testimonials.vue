<script setup lang="ts">
import BaseButton from './BaseButton.vue';
import { onBeforeUnmount, onMounted, ref } from 'vue';
import Swiper from 'swiper';
import { A11y, Autoplay, Keyboard, Navigation, Pagination } from 'swiper/modules';
import 'swiper/css';

const testimonials = [
  {
    title: 'Page one in four months',
    text: 'Luma rebuilt our SEO from the ground up. We now rank on the first page for every keyword that matters and organic traffic has tripled.',
    name: 'Sarah, B2B SaaS founder',
  },
  {
    title: 'They feel like our team',
    text: 'Always responsive, always transparent. The weekly reporting means we know exactly what our ad spend is doing.',
    name: 'Daniel, Marketing lead',
  },
  {
    title: 'Sales up 25%',
    text: 'Our PPC campaign drove a 50% jump in site visits in the first quarter. Bookings followed straight after.',
    name: 'Marco, Restaurant owner',
  },
  {
    title: 'Creative that converts',
    text: 'Our social content finally looks like us, and it sells. Follower growth and online revenue are both up since we started.',
    name: 'Aisha, E-commerce director',
  },
];

const flowPath = (n: number) =>
  `M0,${260 + n * 18} C300,${120 + n * 30} 520,${460 - n * 20} 760,${300 + n * 6} S1180,${80 + n * 25} 1440,${230 + n * 22}`;

const container = ref<HTMLElement | null>(null);
const prevBtn = ref<InstanceType<typeof BaseButton> | null>(null);
const nextBtn = ref<InstanceType<typeof BaseButton> | null>(null);
const dotsEl = ref<HTMLElement | null>(null);
let swiper: Swiper | null = null;

onMounted(() => {
  if (!container.value) return;
  swiper = new Swiper(container.value, {
    modules: [Navigation, Pagination, Autoplay, Keyboard, A11y],
    slidesPerView: 1,
    spaceBetween: 24,
    loop: true,
    speed: 600,
    grabCursor: true,
    autoplay: { delay: 5000, pauseOnMouseEnter: true, disableOnInteraction: false },
    keyboard: { enabled: true, onlyInViewport: true },
    navigation: { prevEl: prevBtn.value?.el ?? null, nextEl: nextBtn.value?.el ?? null },
    pagination: { el: dotsEl.value, clickable: true },
    breakpoints: { 640: { slidesPerView: 2 } },
  });
});

onBeforeUnmount(() => swiper?.destroy(true, true));
</script>

<template>
  <section class="relative overflow-hidden py-20 lg:py-28">
    <!-- neon edge bars -->
    <div class="absolute left-0 top-10 bottom-10 w-3 lg:w-5 bg-luma-v opacity-80" aria-hidden="true" />
    <div class="absolute right-0 top-10 bottom-10 w-3 lg:w-5 bg-luma-v opacity-80" aria-hidden="true" />

    <!-- flowing neon lines -->
    <svg class="absolute inset-x-0 bottom-0 w-full h-[70%] pointer-events-none" viewBox="0 0 1440 500"
      preserveAspectRatio="none" aria-hidden="true">
      <defs>
        <linearGradient id="flow" x1="0" x2="1">
          <stop offset="0" stop-color="#2bff88" />
          <stop offset="0.4" stop-color="#00d4ff" />
          <stop offset="0.7" stop-color="#7b3bff" />
          <stop offset="1" stop-color="#ff2fd6" />
        </linearGradient>
      </defs>
      <path v-for="n in 7" :key="n" :d="flowPath(n)" fill="none" stroke="url(#flow)" stroke-width="1.2"
        :stroke-opacity="0.35 + n * 0.08" vector-effect="non-scaling-stroke" />
    </svg>

    <div class="relative px-8 md:px-14 lg:px-24 grid lg:grid-cols-2 gap-12 lg:gap-10 items-start">
      <div ref="container" class="swiper luma-swiper w-full order-2 lg:order-1">
        <div class="swiper-wrapper">
          <figure v-for="(t, i) in testimonials" :key="t.name" class="swiper-slide flex! flex-col p-7 min-h-[300px]"
            :class="i % 2 ? 'bg-[#4a4a50]' : 'bg-[#3a3a3e]'">
            <span class="font-display text-5xl leading-none font-bold text-gradient" aria-hidden="true">&ldquo;</span>
            <blockquote class="mt-3">
              <p class="font-display text-sm font-semibold">&ldquo;{{ t.title }}&rdquo;</p>
              <p class="mt-4 text-sm text-white/75 leading-relaxed">{{ t.text }}</p>
            </blockquote>
            <figcaption class="label mt-auto pt-5">&mdash;{{ t.name }}</figcaption>
          </figure>
        </div>
      </div>

      <div class="order-1 lg:order-2 lg:pl-10">
        <h2 class="h-display text-4xl lg:text-6xl">
          What they<br />
          <span class="text-outline-white">say about us</span>
        </h2>
      </div>
    </div>

    <div class="relative mt-14 flex items-center justify-center gap-5">
      <BaseButton ref="prevBtn" square icon="arrow-left" aria-label="Previous testimonial" />
      <div ref="dotsEl" class="luma-dots w-auto!" />
      <BaseButton ref="nextBtn" square icon="arrow-right" aria-label="Next testimonial" />
    </div>
  </section>
</template>
