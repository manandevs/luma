<script setup lang="ts">
import About from './components/About.vue';
import Banner from './components/Banner.vue';
import Clients from './components/Clients.vue';
import ContactForm from './components/ContactForm.vue';
import FeaturedWork from './components/FeaturedWork.vue';
import Footer from './components/Footer.vue';
import GetInTouch from './components/GetInTouch.vue';
import Header from './components/Header.vue';
import Hero from './components/Hero.vue';
import LumaWay from './components/LumaWay.vue';
import Stats from './components/Stats.vue';
import Testimonials from './components/Testimonials.vue';
import WaveMesh from './components/WaveMesh.vue';
</script>

<template>
  <Header />
  <main>
    <Hero />
    <About />
    <Banner />
    <LumaWay />
    <WaveMesh :height="240" />
    <Clients />
    <Testimonials />
    <FeaturedWork />
    <ContactForm />
    <Stats />
    <GetInTouch />
  </main>
  <Footer />
</template>
