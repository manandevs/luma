<script setup lang="ts">
import BaseButton from "./BaseButton.vue";

const services = ["SEO", "PPC", "Social", "Email", "Content", "Analytics"];

// Sparkline for the snapshot card (viewBox 280x72).
const trend = [58, 54, 56, 47, 49, 40, 36, 38, 27, 22, 18, 9];
const linePath = trend
  .map((y, i) => `${i ? "L" : "M"}${(i * 280) / (trend.length - 1)},${y}`)
  .join(" ");
const areaPath = `${linePath} L280,72 L0,72 Z`;
</script>

<template>
  <section
    class="relative overflow-hidden min-h-150 flex items-center"
  >
    <!-- Perspective "room" of neon gradient walls -->
    <div
      class="absolute inset-0 pointer-events-none [perspective:1200px]"
      aria-hidden="true"
    >
      <div
        class="absolute right-0 top-[6%] h-[88%] w-[52%] origin-right [transform:rotateY(-52deg)] bg-[linear-gradient(225deg,#ff2fd6_0%,#b62cff_45%,#7b3bff_80%,#00d4ff_100%)] opacity-90"
      />
      <div
        class="absolute left-1/2 -translate-x-1/2 bottom-[-30%] w-[120%] h-[60%] bg-[radial-gradient(ellipse_at_center,rgba(123,59,255,0.45),transparent_60%)]"
      />
    </div>

    <!-- Content -->
    <div
      class="relative w-full px-5 md:px-12 lg:px-20 pt-14 pb-10 lg:pb-16 grid lg:grid-cols-[minmax(0,1fr)_340px] gap-12 lg:gap-10 items-center"
    >
      <div class="flex flex-col items-start">
        <span
          class="label inline-flex items-center gap-2.5 border border-white/25 bg-black/60 backdrop-blur px-4 py-2"
        >
          <span class="relative flex w-2 h-2">
            <span class="absolute inset-0 bg-neon animate-ping opacity-75" />
            <span class="relative w-2 h-2 bg-neon" />
          </span>
          <span>
            Digital growth agency<span class="hidden sm:inline"
              >&nbsp;&middot; Powered by Suggui</span
            >
          </span>
        </span>

        <h1
          class="h-display mt-7 text-[52px] sm:text-[84px] lg:text-[clamp(64px,calc(13.5vw-72px),128px)] leading-[0.9]"
        >
          <span class="block text-stripes">Built for</span>
          <span class="block text-stripes">growth</span>
        </h1>

        <p
          class="mt-7 max-w-2xl text-base lg:text-xl text-white/75 leading-relaxed"
        >
          The next-generation digital marketing partner. We combine SEO, paid
          media, social and content into one strategy — so every channel pulls
          in the same direction:
          <span class="text-white font-semibold">revenue</span>.
        </p>

        <div class="mt-9 flex flex-col sm:flex-row sm:flex-wrap gap-3 w-full sm:w-auto">
          <BaseButton
            href="https://suggui.vercel.app/"
            variant="primary"
            icon="arrow-right"
          >
            Book a free consultation
          </BaseButton>
          <BaseButton href="#way" class="bg-black/60 backdrop-blur">
            Explore services
          </BaseButton>
        </div>
      </div>

      <!-- Growth snapshot card (sits on the purple panel) -->
      <aside
        class="relative w-full max-w-md lg:max-w-none border border-white/25 bg-black/45 backdrop-blur-xl p-6 lg:p-7 shadow-[0_30px_80px_-20px_rgba(0,0,0,0.7)]"
        aria-label="Growth snapshot"
      >
        <span
          class="absolute -top-px -left-px w-10 h-[3px] bg-luma"
          aria-hidden="true"
        />

        <div class="flex items-center justify-between">
          <p class="label text-white/70">Growth snapshot</p>
          <p class="label flex items-center gap-1.5 text-neon">
            <span class="w-1.5 h-1.5 bg-neon" aria-hidden="true" />
            Live results
          </p>
        </div>

        <p class="mt-5 font-display text-5xl font-bold leading-none">
          +200<span class="text-gradient">%</span>
        </p>
        <p class="mt-2 text-sm text-white/70">
          Average organic traffic growth for our clients.
        </p>

        <svg
          class="mt-5 w-full h-[72px]"
          viewBox="0 0 280 72"
          preserveAspectRatio="none"
          aria-hidden="true"
        >
          <defs>
            <linearGradient id="spark-fill" x1="0" y1="0" x2="0" y2="1">
              <stop offset="0" stop-color="#2bff88" stop-opacity="0.35" />
              <stop offset="1" stop-color="#2bff88" stop-opacity="0" />
            </linearGradient>
            <linearGradient id="spark-line" x1="0" x2="1">
              <stop offset="0" stop-color="#00d4ff" />
              <stop offset="1" stop-color="#2bff88" />
            </linearGradient>
          </defs>
          <path :d="areaPath" fill="url(#spark-fill)" />
          <path
            :d="linePath"
            fill="none"
            stroke="url(#spark-line)"
            stroke-width="2"
            vector-effect="non-scaling-stroke"
          />
        </svg>

        <ul
          class="mt-6 pt-5 border-t border-white/15 grid grid-cols-3 gap-y-3 gap-x-2"
        >
          <li
            v-for="(s, i) in services"
            :key="s"
            class="flex items-baseline gap-1.5 text-xs font-semibold"
          >
            <span class="font-display text-[10px] text-white/40">{{
              String(i + 1).padStart(2, "0")
            }}</span>
            {{ s }}
          </li>
        </ul>

        <dl class="mt-5 pt-5 border-t border-white/15 grid grid-cols-2 gap-4">
          <div class="flex flex-col-reverse">
            <dt class="label text-white/60">Client retention</dt>
            <dd class="mb-1.5 font-display text-2xl font-bold">98%</dd>
          </div>
          <div class="flex flex-col-reverse">
            <dt class="label text-white/60">Average ROAS</dt>
            <dd class="mb-1.5 font-display text-2xl font-bold">5&times;</dd>
          </div>
        </dl>
      </aside>
    </div>
  </section>
</template>
