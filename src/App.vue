<script setup lang="ts">
import SiteConfig from './configs/site.json';
import AuthorInfo from './configs/author.json';

import { Icon } from '@iconify/vue'
// set background
document.body.style.backgroundImage = `url(${SiteConfig['background-img']})`;
</script>

<template>
  <div class="flex h-screen w-screen">
    <div class="md:w-5/16 md:w-max-w-2/3 w-full h-full bg-white/50
                backdrop-blur-2xl border-r border-white/50
                shadow-[10px_0px_30px_rgba(0,0,0,0.25)]
                flex flex-col items-center justify-center">
      <img :src="AuthorInfo.avatar" alt="avatar"
        class="h-40 w-40 rounded-full mb-4 
                border-r border-white/50 shadow-xl">
      <h1 class="text-3xl font-bold mb-4">{{ AuthorInfo.name }}</h1>
      <h1 class="text-lg text-gray-700 mb-6" v-if="AuthorInfo.bio">{{ AuthorInfo.bio }}</h1>
      <div class="flex text-2xl gap-2">
        <template v-for="value in AuthorInfo.links">
          <a :href="value.url" target="_blank" 
              class="group relative text-gray-700 hover:text-gray-900 ransition-all duration-300
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
          class="text-sm text-gray-700 hover:text-gray-900 transition-colors duration-300">{{ value.name }}</a>
      </template>
      <p class="text-sm text-gray-700" v-if="SiteConfig.right">&copy; {{ SiteConfig.right }}</p>
    </footer>
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
