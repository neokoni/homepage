<script setup lang="ts">
import LeftInfo from './router/LeftInfo.vue';
import RightPart from './router/RightPart.vue';
import SiteConfig from './configs/site.json';

document.body.style.backgroundImage = `url(${SiteConfig['background-img']})`;
if (SiteConfig.title) {
  document.title=SiteConfig.title;
}
</script>

<template>
  <div class="flex flex-col h-screen w-screen">
    <LeftInfo />
    <!-- <RightPart /> -->
  </div>
</template>
