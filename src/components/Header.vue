<script setup lang="ts">
import BaseButton from './BaseButton.vue';
import { ref } from 'vue';
import Logo from './Logo.vue';

const isMenuOpen = ref(false);

const links = [
  { label: 'Why Luma', href: '#about' },
  { label: 'The Luma Way', href: '#way' },
  { label: 'Clients', href: '#clients' },
  { label: 'Case Studies', href: '#work' },
  { label: 'Contact', href: '#contact' },
];
</script>

<template>
  <nav class="sticky top-0 z-50 w-full px-5 md:px-12 lg:px-20 py-5 flex items-center justify-between bg-black/60 backdrop-blur-xl">
    <a href="#" aria-label="Luma home" @click="isMenuOpen = false">
      <Logo />
    </a>

    <div class="flex items-center gap-4 lg:gap-8">
      <BaseButton href="https://suggui.vercel.app/" size="sm" class="hidden sm:inline-flex">Request a quote</BaseButton>

      <button class="flex items-center gap-3 label" :aria-expanded="isMenuOpen" @click="isMenuOpen = !isMenuOpen">
        {{ isMenuOpen ? 'Close' : 'Menu' }}
        <span class="relative w-6 h-3 block">
          <span class="absolute left-0 w-full h-[2px] bg-white transition-all duration-300"
            :class="isMenuOpen ? 'top-1/2 -translate-y-1/2 rotate-45' : 'top-0'" />
          <span class="absolute left-0 w-full h-[2px] bg-white transition-all duration-300"
            :class="isMenuOpen ? 'top-1/2 -translate-y-1/2 -rotate-45' : 'bottom-0'" />
        </span>
      </button>
    </div>
  </nav>

  <Transition enter-from-class="opacity-0" leave-to-class="opacity-0" enter-active-class="transition-opacity duration-300"
    leave-active-class="transition-opacity duration-300">
    <div v-if="isMenuOpen" class="fixed inset-0 z-40 bg-black pt-28 px-5 md:px-12 lg:px-20 flex flex-col">
      <div class="absolute inset-x-0 top-0 h-1 bg-luma" />
      <ul class="flex flex-col gap-3">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" class="h-display text-4xl md:text-6xl text-outline-white hover:text-white transition-colors"
            @click="isMenuOpen = false">{{ link.label }}</a>
        </li>
      </ul>
      <BaseButton href="https://suggui.vercel.app/" variant="primary" icon="arrow-right" class="mt-10 self-start sm:hidden">
        Request a quote
      </BaseButton>
    </div>
  </Transition>
</template>
