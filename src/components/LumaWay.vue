<script setup lang="ts">
import BaseButton from './BaseButton.vue';
const labs = [
  {
    title: 'The Search Lab',
    text: 'Our SEO engine room. Technical audits, content that ranks and link strategies that put you on page one for the keywords that actually convert.',
  },
  {
    title: 'The Paid Lab',
    text: 'Dedicated media strategists running PPC and paid social across Google, Meta and LinkedIn — optimised daily for cost-per-acquisition, not vanity clicks.',
  },
  {
    title: 'The Data Lab',
    text: 'We treat data like gold. Analytics, tracking and dashboards that show exactly what every pound of spend returns — so you can double down with confidence.',
  },
];

const values = [
  {
    title: 'Clients are partners',
    text: 'We believe in treating our clients like a part of the team. We know that if we have the best relationships we will have the best results.',
  },
  {
    title: 'Strategy first',
    text: 'On-demand strategic advice. Whether you’re launching or scaling, we’re here to help — it’s not about one-off campaigns, it’s about playing the long game.',
  },
  {
    title: 'Humans beat robots',
    text: 'We leverage automation and AI where it helps, but creativity and judgement are what win markets. That’s why we invest in people first.',
  },
];

const services = ['SEO', 'PPC', 'Social', 'Email', 'Content', 'Analytics'];
</script>

<template>
  <section id="way" class="px-5 md:px-12 lg:px-20 py-20 lg:py-28 scroll-mt-24">
    <h2 class="h-display text-5xl lg:text-7xl text-center">
      The Luma<br />
      <span class="text-outline-white">Way</span>
    </h2>

    <div class="mt-14 lg:mt-20 grid lg:grid-cols-2 border border-line">
      <div class="lg:border-r border-line">
        <article v-for="lab in labs" :key="lab.title" class="p-6 lg:p-10 border-b border-line last:border-b-0">
          <h3 class="label text-neon text-xs">{{ lab.title }}</h3>
          <p class="mt-3 text-sm text-white/70 leading-relaxed max-w-md">{{ lab.text }}</p>
        </article>
      </div>
      <div class="border-t lg:border-t-0 border-line">
        <article v-for="(value, i) in values" :key="value.title" class="p-6 lg:p-10 border-b border-line last:border-b-0">
          <h3 class="label text-xs" :class="['text-aqua', 'text-violet', 'text-magenta'][i]">{{ value.title }}</h3>
          <p class="mt-3 text-sm text-white/70 leading-relaxed max-w-md">{{ value.text }}</p>
        </article>
      </div>
    </div>

    <div class="mt-10 flex flex-wrap justify-center gap-3">
      <BaseButton v-for="s in services" :key="s" href="#contact" size="sm" class="min-w-[110px]">{{ s }}</BaseButton>
    </div>
  </section>
</template>
