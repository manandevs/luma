<script setup lang="ts">
import { useId } from 'vue';

// Luma mark: a black "L" cut from the brand gradient, with a square of light at its shoulder.
withDefaults(defineProps<{ markOnly?: boolean }>(), { markOnly: false });

const gradId = `luma-grad-${useId()}`;
</script>

<template>
  <span class="inline-flex items-center gap-2.5">
    <svg viewBox="0 0 32 32" class="w-8 h-8 shrink-0" aria-hidden="true">
      <defs>
        <linearGradient :id="gradId" x1="0" y1="1" x2="1" y2="0">
          <stop offset="0" stop-color="#2bff88" />
          <stop offset="0.35" stop-color="#00d4ff" />
          <stop offset="0.7" stop-color="#7b3bff" />
          <stop offset="1" stop-color="#ff2fd6" />
        </linearGradient>
      </defs>
      <rect width="32" height="32" :fill="`url(#${gradId})`" />
      <path d="M8 6h5.5v14.5H24V26H8z" fill="#000" />
      <rect x="18.5" y="6" width="5.5" height="5.5" fill="#000" />
    </svg>
    <span v-if="!markOnly" class="font-display text-2xl lg:text-[26px] font-bold tracking-tight lowercase leading-none whitespace-nowrap">
      luma<span class="inline-block w-[0.22em] h-[0.22em] ml-[0.06em] bg-luma align-baseline" />
    </span>
  </span>
</template>
