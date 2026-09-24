<script setup lang="ts">
import { computed, ref } from 'vue';

type Variant = 'primary' | 'outline' | 'gradient' | 'ghost';
type Size = 'sm' | 'md' | 'lg';
type Icon = 'arrow-right' | 'arrow-left' | 'arrow-up-right';

const props = withDefaults(defineProps<{
  /** primary: white → gradient sweep · outline: hollow → white fill · gradient: brand gradient → white · ghost: text + underline */
  variant?: Variant;
  size?: Size;
  /** Renders an <a> when set, otherwise a <button>. External http(s) links open in a new tab. */
  href?: string;
  type?: 'button' | 'submit' | 'reset';
  icon?: Icon;
  /** Icon-only square button (give it an aria-label). */
  square?: boolean;
  /** Full width. */
  block?: boolean;
  disabled?: boolean;
}>(), {
  variant: 'outline',
  size: 'md',
  type: 'button',
});

// Exposed so parents (e.g. Swiper navigation) can reach the DOM node.
const el = ref<HTMLElement | null>(null);
defineExpose({ el });

const isExternal = computed(() => !!props.href && /^https?:\/\//.test(props.href));

const iconPaths: Record<Icon, string> = {
  'arrow-right': 'M3 8h10M9 4l4 4-4 4',
  'arrow-left': 'M13 8H3M7 4 3 8l4 4',
  'arrow-up-right': 'M4 12 12 4M5.5 4H12v6.5',
};
</script>

<template>
  <component
    :is="href ? 'a' : 'button'"
    ref="el"
    :href="href && !disabled ? href : undefined"
    :type="href ? undefined : type"
    :target="isExternal ? '_blank' : undefined"
    :rel="isExternal ? 'noopener noreferrer' : undefined"
    :disabled="!href && disabled ? true : undefined"
    :aria-disabled="disabled || undefined"
    :class="['btn', `btn--${variant}`, `btn--${size}`, { 'btn--square': square, 'btn--block': block, 'is-disabled': disabled }]"
  >
    <span v-if="!square" class="btn__label"><slot /></span>
    <svg v-if="icon" :class="['btn__icon', `btn__icon--${icon}`]" viewBox="0 0 16 16" fill="none" stroke="currentColor"
      stroke-width="1.6" stroke-linecap="square" aria-hidden="true">
      <path :d="iconPaths[icon]" />
    </svg>
  </component>
</template>

<style scoped>
/* Layered so Tailwind utilities on the component (hidden, mt-*, w-*) still win. */
@layer components {
  .btn {
    position: relative;
    isolation: isolate;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 0.75rem;
    overflow: hidden;
    font-family: var(--font-display);
    font-weight: 600;
    line-height: 1;
    text-transform: uppercase;
    white-space: nowrap;
    cursor: pointer;
    user-select: none;
    /* Hard offset "block" shadow; the button presses into it on hover/click. */
    --lift: 6px;
    --shadow-color: #444449;
    border: 2px solid transparent;
    box-shadow: var(--lift) var(--lift) 0 var(--shadow-color);
    transition: color 0.35s, border-color 0.35s, box-shadow 0.2s, transform 0.2s;
  }
  .btn:active {
    transform: translate(var(--lift), var(--lift));
    box-shadow: 0 0 0 var(--shadow-color);
  }
  .btn:focus-visible {
    outline: 2px solid #00d4ff;
    outline-offset: 3px;
  }

  /* Overlay that fades in on hover */
  .btn::before {
    content: '';
    position: absolute;
    inset: 0;
    z-index: -1;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  .btn:hover::before,
  .btn:focus-visible::before {
    opacity: 1;
  }

  /* Sizes */
  /* Fixed heights, capped at 40px (max-h-10) */
  .btn--sm { font-size: 10px; height: 2rem; padding: 0 0.9rem; --lift: 4px; }
  .btn--md { font-size: 10px; height: 2.25rem; padding: 0 1.2rem; --lift: 4px; }
  .btn--lg { font-size: 11px; height: 2.5rem; padding: 0 1.5rem; --lift: 5px; }
  .btn--square { padding: 0; aspect-ratio: 1; --lift: 4px; }
  .btn--square.btn--sm { width: 2rem; }
  .btn--square.btn--md { width: 2.25rem; }
  .btn--square.btn--lg { width: 2.5rem; }
  .btn--block { display: flex; width: 100%; }

  /* Variants */
  .btn--primary {
    background: #fff;
    border-color: #fff;
    color: #000;
  }
  .btn--primary::before {
    background: linear-gradient(90deg, #2bff88, #00d4ff 35%, #7b3bff 70%, #ff2fd6);
  }

  .btn--outline {
    background: #000;
    border-color: #fff;
    color: #fff;
  }
  .btn--outline::before {
    background: #fff;
  }
  .btn--outline:hover,
  .btn--outline:focus-visible {
    color: #000;
  }

  .btn--gradient {
    background: linear-gradient(90deg, #2bff88, #00d4ff 35%, #7b3bff 70%, #ff2fd6);
    border-color: #fff;
    color: #000;
  }
  .btn--gradient::before {
    background: #fff;
  }

  .btn--ghost,
  .btn--ghost:hover,
  .btn--ghost:active {
    border: 0;
    box-shadow: none;
    transform: none;
  }
  .btn--ghost {
    padding-inline: 0;
    padding-bottom: 0.6em;
    color: #fff;
  }
  .btn--ghost::after {
    content: '';
    position: absolute;
    inset: auto 0 0 0;
    height: 1px;
    background: rgba(255, 255, 255, 0.3);
  }
  .btn--ghost::before {
    inset: auto 0 0 0;
    height: 2px;
    z-index: 1;
    background: linear-gradient(90deg, #2bff88, #00d4ff 35%, #7b3bff 70%, #ff2fd6);
  }

  /* Icon nudges toward its direction on hover */
  .btn__icon {
    width: 1.25em;
    height: 1.25em;
    flex-shrink: 0;
    transition: transform 0.35s cubic-bezier(0.7, 0, 0.2, 1);
  }
  .btn--square .btn__icon {
    width: 0.95rem;
    height: 0.95rem;
  }
  .btn:hover .btn__icon--arrow-right { transform: translateX(4px); }
  .btn:hover .btn__icon--arrow-left { transform: translateX(-4px); }
  .btn:hover .btn__icon--arrow-up-right { transform: translate(3px, -3px); }
  .btn--square:hover .btn__icon { transform: none; }

  .btn.is-disabled {
    opacity: 0.4;
    pointer-events: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .btn,
  .btn::before,
  .btn__icon {
    transition: none;
  }
}
</style>
