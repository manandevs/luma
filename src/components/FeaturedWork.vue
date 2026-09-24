<script setup lang="ts">
import BaseButton from './BaseButton.vue';
import { onBeforeUnmount, onMounted, ref } from 'vue';
import Swiper from 'swiper';
import { A11y, Autoplay, Keyboard, Navigation, Pagination } from 'swiper/modules';
import 'swiper/css';

const cases = [
  {
    sector: 'Local business',
    title: 'Restaurant PPC Growth',
    tags: ['PPC', 'Local SEO', 'Landing pages'],
    result: '+50% website traffic, +25% sales',
  },
  {
    sector: 'B2B startup',
    title: 'SaaS Organic Search',
    tags: ['SEO', 'Content', 'Technical audit'],
    result: 'Page-one rankings, +200% organic traffic',
  },
  {
    sector: 'E-commerce',
    title: 'Retail Social Campaign',
    tags: ['Paid social', 'Creative', 'Community'],
    result: '+25% followers, +20% online sales',
  },
  {
    sector: 'Professional services',
    title: 'Lead Gen Email Engine',
    tags: ['Email', 'Automation', 'CRM'],
    result: '3x qualified leads per month',
  },
];

const container = ref<HTMLElement | null>(null);
const prevBtn = ref<InstanceType<typeof BaseButton> | null>(null);
const nextBtn = ref<InstanceType<typeof BaseButton> | null>(null);
const dotsEl = ref<HTMLElement | null>(null);
let swiper: Swiper | null = null;

onMounted(() => {
  if (!container.value) return;
  swiper = new Swiper(container.value, {
    modules: [Navigation, Pagination, Autoplay, Keyboard, A11y],
    slidesPerView: 1.1,
    spaceBetween: 20,
    loop: true,
    speed: 600,
    grabCursor: true,
    autoplay: { delay: 4500, pauseOnMouseEnter: true, disableOnInteraction: false },
    keyboard: { enabled: true, onlyInViewport: true },
    navigation: { prevEl: prevBtn.value?.el ?? null, nextEl: nextBtn.value?.el ?? null },
    pagination: { el: dotsEl.value, clickable: true },
    breakpoints: {
      640: { slidesPerView: 2 },
      1024: { slidesPerView: 3 },
    },
  });
});

onBeforeUnmount(() => swiper?.destroy(true, true));
</script>

<template>
  <section id="work" class="px-5 md:px-12 lg:px-20 py-16 scroll-mt-24">
    <div class="relative bg-luma pt-10 lg:pt-14 overflow-hidden">
      <!-- giant hollow side words -->
      <span class="hidden lg:block absolute -left-6 top-4 h-display text-[140px] text-outline-black opacity-60 select-none"
        aria-hidden="true">Re</span>
      <span class="hidden lg:block absolute -right-10 top-4 h-display text-[140px] text-outline-black opacity-60 select-none"
        aria-hidden="true">Sult</span>

      <h2 class="relative h-display text-3xl sm:text-5xl lg:text-6xl text-center text-black px-4">
        <span class="text-outline-black bg-white px-2 mb-1 leading-[0.75]">Featured work</span><br />
        and real results
      </h2>

      <div class="relative mt-10 px-5 lg:px-14 pb-8">
        <div ref="container" class="swiper luma-swiper">
          <div class="swiper-wrapper">
            <article v-for="c in cases" :key="c.title" class="swiper-slide flex! bg-black min-h-[340px]">
              <div class="w-4 shrink-0 bg-luma-v flex items-center justify-center">
              </div>
              <div class="p-6 flex flex-col flex-1">
                <p class="label text-white/60">{{ c.sector }}</p>
                <h3 class="mt-2 font-display text-lg font-bold uppercase leading-tight">{{ c.title }}</h3>
                <p class="mt-5 text-xs text-neon flex flex-wrap gap-x-2 gap-y-1">
                  <template v-for="(tag, i) in c.tags" :key="tag">
                    <span v-if="i" class="text-white/30">|</span><span>{{ tag }}</span>
                  </template>
                </p>
                <p class="mt-5 mb-8 text-sm text-white/80">{{ c.result }}</p>
                <BaseButton href="#contact" size="sm" icon="arrow-up-right" class="mt-auto self-center">View more</BaseButton>
              </div>
            </article>
          </div>
        </div>
        <div ref="dotsEl" class="luma-dots on-light justify-center mt-6" />
      </div>
      <div class="h-4 bg-[linear-gradient(90deg,#ff2fd6,#7b3bff)]" />
    </div>

    <div class="mt-8 flex justify-center gap-3">
      <BaseButton ref="prevBtn" square icon="arrow-left" aria-label="Previous case study" />
      <BaseButton ref="nextBtn" square icon="arrow-right" aria-label="Next case study" />
    </div>
  </section>
</template>
