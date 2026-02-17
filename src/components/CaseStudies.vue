<script setup lang="ts">
import { ref } from 'vue';

// --- Data: CTA Section ---
const ctaContent = {
  title: "Let’s make things happen",
  description: "Contact us today to learn more about how Luma's digital marketing services can help your business grow and succeed online.",
  buttonText: "Get your free proposal"
};

// --- Data: Case Studies ---
const caseStudies = [
  {
    title: "Local Business",
    text: "For a local restaurant, we implemented a targeted PPC campaign that resulted in a 50% increase in website traffic and a 25% increase in sales.",
  },
  {
    title: "B2B Startup",
    text: "For a B2B software company, we developed an SEO strategy that resulted in a first page ranking for key keywords and a 200% increase in organic traffic.",
  },
  {
    title: "E-Commerce",
    text: "For a national retail chain, we created a social media marketing campaign that increased followers by 25% and generated a 20% increase in online sales.",
  }
];

// --- Data: Working Process ---
const openProcessIndex = ref<number | null>(0);

const processes = [
  {
    number: '01',
    title: 'Consultation',
    description: 'During the initial consultation, we will discuss your business goals and objectives, target audience, and current marketing efforts.'
  },
  {
    number: '02',
    title: 'Research and Strategy',
    description: 'We conduct deep research to identify the best digital marketing strategies for your specific business niche and competitor landscape.'
  },
  {
    number: '03',
    title: 'Implementation',
    description: 'Once the strategy has been developed and approved, our team begins implementing the services outlined in the plan.'
  },
  {
    number: '04',
    title: 'Monitoring',
    description: 'We continuously monitor performance metrics and optimize campaigns to ensure maximum ROI and sustained growth.'
  }
];

const toggleProcess = (index: number) => {
  openProcessIndex.value = openProcessIndex.value === index ? null : index;
};

const formType = ref('say_hi'); 
</script>

<template>
  <div class="text-black overflow-x-hidden pb-0">

    <!-- Case Studies Section -->
    <section id="cases" class="mt-[140px] px-5 md:px-[100px]">
      <div
        class="flex flex-col lg:flex-row lg:justify-start items-center gap-[30px] lg:gap-10 mb-10 lg:mb-20 text-center lg:text-left">
        <h2 class="text-[36px] lg:text-[40px] font-medium bg-[#008000] text-white px-[7px] rounded-[7px] inline-block">
          Case Studies
        </h2>
        <p class="text-base lg:text-lg max-w-[580px]">
          Explore Real-Life Examples of Our Proven Digital Marketing Success.
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-5 lg:gap-8">
        <div v-for="(caseItem, index) in caseStudies" :key="index"
          class="bg-[#191A23] text-white rounded-[45px] p-[40px] flex flex-col justify-between border border-transparent hover:border-[#008000] hover:-translate-y-2 transition-all duration-300 shadow-[0_5px_0_black] hover:shadow-[0_10px_0_#008000]">

          <div>
            <h4 class="text-[#008000] text-2xl font-medium mb-5 border-b border-white/20 pb-3">{{ caseItem.title }}</h4>
            <p class="text-base lg:text-lg mb-8 text-gray-300">{{ caseItem.text }}</p>
          </div>

          <a href="#" class="text-[#008000] text-xl flex items-center gap-4 group">
            <span class="group-hover:underline">Learn more</span>
            <svg width="19" height="19" viewBox="0 0 19 19" fill="none" xmlns="http://www.w3.org/2000/svg"
              class="rotate-[30deg] group-hover:rotate-0 transition-transform duration-300">
              <path d="M2.07107 16.9289L16.2132 2.7868M16.2132 2.7868V16.5028M16.2132 2.7868H2.49723" stroke="#008000"
                stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
          </a>
        </div>
      </div>
    </section>

    <!-- Working Process Section -->
    <section class="mt-[140px] px-5 md:px-[100px]">
      <div
        class="flex flex-col lg:flex-row lg:justify-start items-center gap-[30px] lg:gap-10 mb-10 lg:mb-20 text-center lg:text-left">
        <h2
          class="text-[36px] lg:text-[40px] font-medium bg-[#008000] text-white px-[7px] rounded-[7px] inline-block text-center lg:whitespace-nowrap">
          Our Working Process
        </h2>
        <p class="text-base lg:text-lg max-w-[292px]">
          Step-by-Step Guide to Achieving Your Business Goals
        </p>
      </div>

      <div class="flex flex-col gap-5 lg:gap-[30px]">
        <div v-for="(process, index) in processes" :key="index" @click="toggleProcess(index)" :class="[
          'border-2 rounded-[45px] p-[30px] lg:px-[60px] lg:py-[41px] transition-all duration-300 cursor-pointer',
          openProcessIndex === index
            ? 'bg-white border-[#008000] shadow-[0_5px_0_#008000]'
            : 'bg-[#F3F3F3] border-black shadow-[0_5px_0_#191A23]'
        ]">

          <!-- Accordion Header -->
          <div class="flex justify-between items-center"
            :class="{ 'border-b border-black/10 pb-[15px] lg:pb-[30px] mb-[15px] lg:mb-[30px]': openProcessIndex === index }">
            <div class="flex items-center gap-[20px] lg:gap-[35px]">
              <span class="text-[30px] lg:text-[60px] font-medium"
                :class="openProcessIndex === index ? 'text-[#008000]' : 'text-black'">{{ process.number }}</span>
              <span class="text-[18px] lg:text-[30px] font-medium text-black">{{ process.title }}</span>
            </div>

            <!-- Toggle Icon -->
            <div
              class="w-[30px] h-[30px] lg:w-[58px] lg:h-[58px] rounded-full border border-black flex items-center justify-center bg-white transition-transform duration-300"
              :class="{ 'rotate-180 bg-[#008000] border-transparent': openProcessIndex === index }">
              <span v-if="openProcessIndex !== index" class="text-2xl lg:text-4xl text-black">+</span>
              <span v-else class="text-2xl lg:text-4xl text-white">-</span>
            </div>
          </div>

          <!-- Accordion Body -->
          <div v-show="openProcessIndex === index">
            <p class="text-base lg:text-lg pt-5 lg:pt-0 text-black/80">
              {{ process.description }}
            </p>
          </div>
        </div>
      </div>
    </section>on>

    <!-- Contact Us Section -->
    <section class="mt-[140px] px-5 md:px-[100px] mb-[140px]">
      <div
        class="flex flex-col lg:flex-row lg:justify-start items-center gap-[30px] lg:gap-10 mb-10 lg:mb-20 text-center lg:text-left">
        <h2 class="text-[36px] lg:text-[40px] font-medium bg-[#008000] text-white px-[7px] rounded-[7px] inline-block">
          Contact Us</h2>
        <p class="text-base lg:text-lg max-w-[323px]">
          Connect with Us: Let's Discuss Your Digital Marketing Needs
        </p>
      </div>

      <div
        class="bg-[#F3F3F3] rounded-[45px] p-[30px] lg:p-[60px] lg:px-[100px] relative overflow-hidden shadow-[0_5px_0_#191A23] border border-black">
        <form class="flex flex-col gap-9 max-w-[556px] relative z-10" @submit.prevent>

          <div class="flex gap-[35px]">
            <div class="flex items-center gap-[14px]">
              <label class="cursor-pointer flex items-center gap-[14px]">
                <input type="radio" name="type" value="say_hi" v-model="formType" class="hidden">
                <div
                  class="w-[26px] h-[26px] rounded-full border border-black bg-white flex items-center justify-center p-[5px]">
                  <div v-if="formType === 'say_hi'" class="w-full h-full rounded-full bg-[#008000]"></div>
                </div>
                <span>Say Hi</span>
              </label>
            </div>
            <div class="flex items-center gap-[14px]">
              <label class="cursor-pointer flex items-center gap-[14px]">
                <input type="radio" name="type" value="quote" v-model="formType" class="hidden">
                <div
                  class="w-[26px] h-[26px] rounded-full border border-black bg-white flex items-center justify-center p-[5px]">
                  <div v-if="formType === 'quote'" class="w-full h-full rounded-full bg-[#008000]"></div>
                </div>
                <span>Get a Quote</span>
              </label>
            </div>
          </div>

          <div class="flex flex-col gap-[25px]">
            <div class="flex flex-col gap-[10px]">
              <label class="text-base font-normal">Name</label>
              <input type="text" placeholder="Name"
                class="w-full px-[30px] py-[18px] border border-black rounded-[14px] bg-white placeholder:text-gray-500 focus:outline-none focus:ring-1 focus:ring-[#008000]">
            </div>
            <div class="flex flex-col gap-[10px]">
              <label class="text-base font-normal">Email*</label>
              <input type="email" placeholder="Email"
                class="w-full px-[30px] py-[18px] border border-black rounded-[14px] bg-white placeholder:text-gray-500 focus:outline-none focus:ring-1 focus:ring-[#008000]">
            </div>
            <div class="flex flex-col gap-[10px]">
              <label class="text-base font-normal">Message*</label>
              <textarea rows="6" placeholder="Message"
                class="w-full px-[30px] py-[18px] border border-black rounded-[14px] bg-white placeholder:text-gray-500 focus:outline-none focus:ring-1 focus:ring-[#008000]"></textarea>
            </div>
          </div>

          <button type="submit"
            class="w-full bg-[#191A23] text-white py-5 rounded-[14px] text-xl hover:bg-black/80 transition-colors">Send
            Message</button>
        </form>

        <div class="hidden lg:block absolute top-1/2 -translate-y-1/2 -right-[150px]">
          <img src="https://placehold.co/500x500/008000/FFFFFF?text=Luma" alt="Contact Illustration"
            class="opacity-100 rotate-12 rounded-full border-4 border-black">
        </div>
      </div>
    </section>

    <!-- NEW SIMPLE FOOTER -->
    <footer class="bg-[#191A23] text-white py-8 border-t border-[#008000]">
      <div
        class="max-w-[1440px] mx-auto px-5 md:px-[100px] flex flex-col md:flex-row justify-between items-center gap-4">

        <!-- Logo -->
        <div class="flex items-center gap-2">
          <svg width="24" height="24" viewBox="0 0 36 36" fill="#008000" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M17.999 5.535l17.6-5.186L30.465 18 35.6 35.601l-17.601-5.136L.348 35.602l5.185-17.6L.348.348l17.65 5.186z" />
          </svg>
          <span class="text-xl font-semibold">Luma</span>
        </div>

        <!-- Copyright -->
        <p class="text-sm opacity-60">© 2023 Luma. All Rights Reserved.</p>

        <!-- Simple Link -->
        <a href="#" class="text-sm underline hover:text-[#008000] transition-colors">Privacy Policy</a>
      </div>
    </footer>

  </div>
</template>

<style scoped>
.no-scrollbar::-webkit-scrollbar {
  display: none;
}

.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>