<template>
    <div class="bg-white/50 border-white/50
                dark:bg-black/60 dark:border-gray-700/50
                backdrop-blur-2xl border p-2
                text-black/85 dark:text-gray-300
                rounded-tl-lg text-sm">
        <p>Background Info</p>
        <p v-if="backgroundInfo[+prop.darkMod]?.author">Author: <a :href="backgroundInfo[+prop.darkMod]?.authorUrl" target="_blank">
          {{ backgroundInfo[+prop.darkMod]?.author }}
          </a>
        </p>
        
        <p v-if="backgroundInfo[+prop.darkMod]?.name">Source: <a :href="backgroundInfo[+prop.darkMod]?.imgSource" target="_blank">
          {{ backgroundInfo[+prop.darkMod]?.name }}
        </a>
        </p>
    </div>
</template>

<script setup lang="ts">
import SiteConfig from '../configs/site.json';

type BackgroundInfo = {
  author: string;
  authorUrl: string;
  imgSource: string;
  name: string;
}
const backgroundInfo = SiteConfig.backgroundInfo as BackgroundInfo[];
const prop = defineProps<{
  darkMod: boolean;
}>();
</script>