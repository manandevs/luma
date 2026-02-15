<script setup lang="ts">
interface Service {
  title: string[];
  theme: 'grey' | 'green' | 'black';
  image: string;
}

const services: Service[] = [
  {
    title: ['Search engine', 'optimization'],
    theme: 'grey',
    image: '/images/card-seo.png',
  },
  {
    title: ['Pay-per-click', 'advertising'],
    theme: 'green',
    image: '/images/card-Pay-per-click.png',
  },
  {
    title: ['Social Media', 'Marketing'],
    theme: 'black',
    image: '/images/card-social-media.png',
  },
  {
    title: ['Email', 'Marketing'],
    theme: 'grey',
    image: '/images/card-email.png',
  },
  {
    title: ['Content', 'Creation'],
    theme: 'green',
    image: '/images/card-content-creation.png',
  },
  {
    title: ['Analytics and', 'Tracking'],
    theme: 'black',
    image: '/images/card-analytics-tracking.png',
  },
];

const getThemeClasses = (theme: string) => {
  switch (theme) {
    case 'green':
      return {
        card: 'bg-[#008000]',
        textBg: 'bg-[#191A23]',
        titleColor: 'text-white',
        buttonBg: 'bg-white', 
        arrowColor: 'text-[#191A23]', 
        textColor: 'text-black',
        shadow: 'shadow-[0_5px_0_#008000]'
      };
    case 'black':
      return {
        card: 'bg-[#191A23]',
        textBg: 'bg-white',
        titleColor: 'text-black',
        buttonBg: 'bg-black', 
        arrowColor: 'text-white', 
        textColor: 'text-white',
        shadow: 'shadow-[0_5px_0_#191A23]'
      };
    case 'grey':
    default:
      return {
        card: 'bg-[#F3F3F3]',
        textBg: 'bg-[#008000]',
        titleColor: 'text-white',
        buttonBg: 'bg-black',
        arrowColor: 'text-[#008000]',
        textColor: 'text-black',
        shadow: 'shadow-[0_5px_0_#F3F3F3]'
      };
  }
};
</script>

<template>
  <section id="services" class="mt-[60px] lg:mt-[140px] px-5 md:px-[100px] text-black">

    <!-- Section Header -->
    <div
      class="flex flex-col lg:flex-row lg:justify-start items-center gap-[30px] lg:gap-10 mb-10 lg:mb-20 text-center lg:text-left">
      <h2 class="text-[36px] lg:text-[40px] font-medium bg-[#008000] px-[7px] rounded-[7px] inline-block text-black">
        Services
      </h2>
      <p class="text-base lg:text-lg max-w-[580px] text-white lg:text-white">
        At Luma, we offer a range of services to help businesses grow and succeed online. These services include:
      </p>
    </div>

    <!-- Grid -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">

      <div v-for="(service, index) in services" :key="index" :class="[
        'border border-black rounded-[45px] flex flex-col lg:flex-row justify-between lg:h-[310px] transition-transform hover:-translate-y-1  overflow-hidden',
        getThemeClasses(service.theme).card,
        getThemeClasses(service.theme).shadow
      ]">
        <div class="flex flex-col justify-between h-full p-[50px]">

          <!-- Title Lines -->
          <div class="flex flex-col items-start">
            <span v-for="(line, i) in service.title" :key="i" :class="[
              'text-[26px] lg:text-[30px] font-medium px-[7px] rounded-[7px]',
              getThemeClasses(service.theme).textBg,
              getThemeClasses(service.theme).titleColor
            ]">
              {{ line }}
            </span>
          </div>

          <a href="#"
            :class="['hidden lg:flex items-center gap-4 text-xl group', getThemeClasses(service.theme).textColor]">
            <div :class="[
              'w-[41px] h-[41px] rounded-full flex items-center justify-center transition-transform group-hover:rotate-12',
              getThemeClasses(service.theme).buttonBg
            ]">
              <svg width="19" height="19" viewBox="0 0 19 19" fill="none" xmlns="http://www.w3.org/2000/svg"
                :class="['rotate-[30deg]', getThemeClasses(service.theme).arrowColor]">
                <path d="M2.07107 16.9289L16.2132 2.7868M16.2132 2.7868V16.5028M16.2132 2.7868H2.49723"
                  stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
            </div>
            <span>Learn more</span>
          </a>
        </div>

        <div class="flex items-end justify-between lg:block overflow-hidden">
          <a href="#" :class="[
            'lg:hidden w-[41px] h-[41px] rounded-full flex items-center justify-center mt-[27px] lg:mt-0',
            getThemeClasses(service.theme).buttonBg
          ]">
            <svg width="19" height="19" viewBox="0 0 19 19" fill="none" xmlns="http://www.w3.org/2000/svg"
              :class="['rotate-[30deg]', getThemeClasses(service.theme).arrowColor]">
              <path d="M2.07107 16.9289L16.2132 2.7868M16.2132 2.7868V16.5028M16.2132 2.7868H2.49723"
                stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
          </a>

          <img :src="service.image" :alt="service.title.join(' ')" class="h-full w-auto object-contain">
        </div>
      </div>

    </div>
  </section>
</template>