<script setup lang="ts">
import SiteConfig from './configs/site.json';
import AuthorInfo from './configs/author.json';

import { Icon } from '@iconify/vue'
import BackgroundInfo from './components/BackgroundInfo.vue';
import { onBeforeUnmount, onMounted, ref } from 'vue';
// set background
var defaultBackground = `url(${SiteConfig['background-img']})`;
var darkBackground = `url(${SiteConfig['darkmode-background-img']})`;
const usingDarkBackground = ref(false);
const setCurrentTheme = () => {
  const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
  usingDarkBackground.value = isDarkMode && darkBackground.length > 5; // url() is 5 characters
}
setCurrentTheme();
document.documentElement.style.setProperty('--default-background', defaultBackground);
document.documentElement.style.setProperty('--dark-background', darkBackground);

let colorSchemeQuery: MediaQueryList | null = null;
const handleColorSchemeChange = () => setCurrentTheme();

onMounted(() => {
  colorSchemeQuery = window.matchMedia('(prefers-color-scheme: dark)');
  if ('addEventListener' in colorSchemeQuery) {
    colorSchemeQuery.addEventListener('change', handleColorSchemeChange);
  } else {
    colorSchemeQuery.addListener(handleColorSchemeChange);
  }
});

onBeforeUnmount(() => {
  if (!colorSchemeQuery) return;
  if ('removeEventListener' in colorSchemeQuery) {
    colorSchemeQuery.removeEventListener('change', handleColorSchemeChange);
  } else {
    colorSchemeQuery.removeListener(handleColorSchemeChange);
  }
});

</script>

<template>
  <div class="flex h-screen w-screen">
    <div class="md:w-5/16 md:w-max-w-2/3 w-full h-full 
                bg-white/50 border-white/50
                dark:bg-black/60 dark:border-gray-700/50
                backdrop-blur-2xl border-r transition-all duration-300
                shadow-[10px_0px_30px_rgba(0,0,0,0.25)]
                flex flex-col items-center justify-center">
      <img :src="AuthorInfo.avatar" alt="avatar"
        class="h-40 w-40 rounded-full mb-4 shadow-xl">
      <h1 class="text-3xl font-bold mb-4
                text-gray-900 dark:text-gray-200">{{ AuthorInfo.name }}</h1>
      <h1 class="text-lg text-gray-700 dark:text-gray-300 mb-6" v-if="AuthorInfo.bio">{{ AuthorInfo.bio }}</h1>
      <div class="flex text-2xl gap-2">
        <template v-for="value in AuthorInfo.links">
          <a :href="value.url" target="_blank" 
              class="text-gray-700 hover:text-gray-900 
                    dark:text-gray-300 dark:hover:text-white
                    ransition-all duration-300 group relative 
                    flex-col flex items-center justify-center hover:ml-2 hover:mr-2"
              :style="{
                '--icon-default': value.defaultColor || undefined,
                '--icon-hover': value.hoverColor || undefined,
              }">
            <Icon :icon="value.icon" class="icon-color" />
            <div class="h-full text-sm absolute pt-10 opacity-0 transition-all duration-200
                        hover:opacity-100">
              {{ value.name }}
            </div>
          </a>
        </template>
      </div>
      <div class="md:h-0 h-10"></div>
    </div>
    <footer class="absolute bottom-0 md:w-5/16 w-full h-[-100px] mb-3
                flex flex-col items-center justify-center">
      <template v-for="value in SiteConfig.icp" v-if="SiteConfig.icp">
        <a :href="value.url" target="_blank"
          class="text-gray-700 hover:text-gray-900
              dark:text-gray-200 dark:hover:text-white
              text-sm transition-colors duration-300">{{ value.name }}</a>
      </template>
      <p class="text-sm text-gray-700 dark:text-gray-100" v-if="SiteConfig.right">&copy; {{ SiteConfig.right }}</p>
    </footer>
    <div v-if="SiteConfig.showBackgroundInfo" 
        class="invisible md:visible right-0 bottom-0 absolute">
        <BackgroundInfo :dark-mod="usingDarkBackground"/>
      </div>
  </div>
</template>

<style scoped>
.icon-color {
  color: var(--icon-default, currentColor);
  transition: color 200ms ease;
}

.group:hover .icon-color {
  color: var(--icon-hover, currentColor);
}
</style>
