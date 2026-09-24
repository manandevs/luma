<script setup lang="ts">
import { computed } from 'vue';

// Wireframe "terrain" lines like the reference's section dividers.
const props = withDefaults(defineProps<{
  lines?: number;
  height?: number;
  gradient?: boolean;
  seed?: number;
}>(), {
  lines: 34,
  height: 260,
  gradient: false,
  seed: 1,
});

const WIDTH = 1440;
const STEP = 10;

const peaks = computed(() => {
  const s = props.seed;
  return [
    { x: 380 + 60 * s, w: 150, h: 0.55 },
    { x: 760 - 40 * s, w: 110, h: 1 },
    { x: 1060 + 30 * s, w: 170, h: 0.75 },
    { x: 1300, w: 90, h: 0.4 },
  ];
});

const paths = computed(() => {
  const out: string[] = [];
  const n = props.lines;
  for (let i = 0; i < n; i++) {
    const t = i / (n - 1);
    const baseY = props.height * (0.35 + 0.6 * t);
    const amp = props.height * 0.55 * Math.sin(Math.PI * (0.15 + 0.85 * t));
    let d = '';
    for (let x = 0; x <= WIDTH; x += STEP) {
      let h = 0;
      for (const p of peaks.value) {
        h += p.h * Math.exp(-(((x - p.x - i * 6) / p.w) ** 2));
      }
      const ripple = 0.75 + 0.25 * Math.sin(x * 0.045 + i * 0.9) * Math.cos(x * 0.013 - i * 0.4);
      const y = baseY - amp * h * ripple;
      d += `${x === 0 ? 'M' : 'L'}${x},${y.toFixed(1)}`;
    }
    out.push(d);
  }
  return out;
});

const gradId = `mesh-${Math.random().toString(36).slice(2, 8)}`;
</script>

<template>
  <svg :viewBox="`0 0 ${WIDTH} ${height}`" preserveAspectRatio="none" class="block w-full" :style="{ height: `${height}px` }"
    aria-hidden="true">
    <defs v-if="gradient">
      <linearGradient :id="gradId" x1="0" x2="1" y1="0" y2="0">
        <stop offset="0" stop-color="#7b3bff" />
        <stop offset="0.5" stop-color="#00d4ff" />
        <stop offset="1" stop-color="#ff2fd6" />
      </linearGradient>
    </defs>
    <path v-for="(d, i) in paths" :key="i" :d="d" fill="none" :stroke="gradient ? `url(#${gradId})` : '#fff'"
      :stroke-opacity="0.25 + 0.6 * (i / lines)" stroke-width="1" vector-effect="non-scaling-stroke" />
  </svg>
</template>
