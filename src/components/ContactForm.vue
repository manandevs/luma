<script setup lang="ts">
import BaseButton from './BaseButton.vue';
import { ref } from 'vue';

const sent = ref(false);
const fieldClass =
  'block w-full bg-transparent text-sm text-white placeholder:text-white/35 mt-2 focus:outline-none';
const boxClass = 'border border-white/70 px-5 py-4 focus-within:border-neon transition-colors';
</script>

<template>
  <section id="contact" class="px-5 md:px-12 lg:px-20 py-20 lg:py-28 scroll-mt-24">
    <h2 class="h-display text-3xl sm:text-5xl lg:text-6xl">
      <span class="text-outline-white">Send us a</span> quick message<br />
      and we&rsquo;ll <span class="text-outline-white">do all the rest</span>
    </h2>

    <form class="mt-12 lg:mt-16 grid gap-5" @submit.prevent="sent = true">
      <div class="grid md:grid-cols-3 gap-5">
        <label :class="boxClass">
          <span class="label">Full name *</span>
          <input required type="text" placeholder="Your full name" :class="fieldClass" />
        </label>
        <label :class="boxClass">
          <span class="label">Your email *</span>
          <input required type="email" placeholder="Your primary email" :class="fieldClass" />
        </label>
        <label :class="boxClass">
          <span class="label">Your phone</span>
          <input type="tel" placeholder="Your contact number" :class="fieldClass" />
        </label>
      </div>

      <div class="grid md:grid-cols-[1fr_2fr] gap-5">
        <label :class="boxClass">
          <span class="label">Your company *</span>
          <input required type="text" placeholder="Company or brand" :class="fieldClass" />
        </label>
        <label :class="[boxClass, 'relative']">
          <span class="label">What do you need?</span>
          <svg class="absolute right-5 bottom-5 pointer-events-none" width="12" height="8" viewBox="0 0 12 8" fill="none"
            stroke="#fff" aria-hidden="true"><path d="M1 1l5 5 5-5" /></svg>
          <select :class="[fieldClass, 'appearance-none cursor-pointer pr-8']">
            <option class="bg-black" value="">Select an option</option>
            <option class="bg-black">SEO</option>
            <option class="bg-black">PPC advertising</option>
            <option class="bg-black">Social media marketing</option>
            <option class="bg-black">Email marketing</option>
            <option class="bg-black">Content creation</option>
            <option class="bg-black">Analytics &amp; tracking</option>
          </select>
        </label>
      </div>

      <label :class="boxClass">
        <span class="label">Anything we should know?</span>
        <textarea rows="3" placeholder="Tell us a little about your goals" :class="[fieldClass, 'resize-none']" />
      </label>

      <div class="flex items-center justify-end gap-5">
        <p v-if="sent" class="text-sm text-neon" role="status">Thanks! We&rsquo;ll be in touch within 24 hours.</p>
        <BaseButton type="submit" variant="gradient" icon="arrow-right" class="min-w-[160px]">Submit</BaseButton>
      </div>
    </form>
  </section>
</template>
