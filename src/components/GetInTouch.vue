<script setup lang="ts">
const rows = [
  { label: 'Email', value: 'hello@luma.agency', href: 'mailto:hello@luma.agency' },
  { label: 'Quote', value: 'suggui.vercel.app', href: 'https://suggui.vercel.app/' },
  { label: 'Response', value: 'Within 24 hours' },
  { label: 'Hours', value: 'Mon – Fri, 9:00 – 18:00' },
  { label: 'Services', value: 'SEO · PPC · Social · Email · Content' },
  { label: 'Powered by', value: 'Suggui', href: 'https://suggui.vercel.app/' },
];
</script>

<template>
  <section class="px-5 md:px-12 lg:px-20 py-10">
    <div class="bg-[linear-gradient(120deg,#7b3bff_0%,#3a5bff_35%,#00d4ff_60%,#b62cff_85%,#ff2fd6_100%)] p-6 md:p-10 lg:p-14">
      <h2 class="h-display text-4xl lg:text-6xl">Get in touch</h2>
      <dl class="mt-8 lg:mt-10 grid md:grid-cols-2 gap-x-16">
        <div v-for="row in rows" :key="row.label"
          class="grid grid-cols-[110px_1fr] gap-4 py-3 border-b border-white/30 text-sm">
          <dt class="label text-white/80 self-center">{{ row.label }}</dt>
          <dd>
            <a v-if="row.href" :href="row.href" class="font-semibold hover:underline">{{ row.value }}</a>
            <span v-else class="font-semibold">{{ row.value }}</span>
          </dd>
        </div>
      </dl>
    </div>
  </section>
</template>
