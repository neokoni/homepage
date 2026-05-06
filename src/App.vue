<script setup lang="ts">
import LeftInfo from './router/LeftInfo.vue';
import RightPart from './router/RightPart.vue';
import SiteConfig from './configs/site.json';

// set background
document.body.style.backgroundImage = `url(${SiteConfig['background-img']})`;
</script>

<template>
  <div class="flex flex-col h-screen w-screen">
    <LeftInfo />
    <!-- <RightPart /> -->
  </div>
</template>
