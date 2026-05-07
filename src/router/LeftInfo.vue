<template>
    <div class="w-5/16 w-max-w-2/3 h-full bg-white/50
                backdrop-blur-2xl border-r border-white/50
                shadow-[10px_0px_30px_rgba(0,0,0,0.25)]
                flex flex-col items-center justify-center">
        <img :src="AuthorInfo.avatar"
             alt="avatar"
             class="h-40 w-40 rounded-full mb-4 
                    border-r border-white/50 shadow-xl">
        <h1 class="text-3xl font-bold mb-4">{{ AuthorInfo.name }}</h1>
        <h1 class="text-lg text-gray-700 mb-6" v-if="AuthorInfo.bio">{{ AuthorInfo.bio }}</h1>
        <div class="flex text-2xl gap-2">
            <template v-for="value in AuthorInfo.links">
                <a :href="value.url" target="_blank"
                    class="group relative text-gray-700 hover:text-gray-900 ransition-all duration-300
                           flex-col flex items-center justify-center hover:ml-2 hover:mr-2"
                     >
                    <Icon :icon="value.icon" />
                    <div class="text-sm absolute pt-10 opacity-0 transition-all duration-200
                                hover:opacity-100">
                        {{ value.name }}
                    </div>
                </a>
            </template>
        </div>
    </div>
    <footer class="absolute bottom-0 w-5/16 h-[-100px] mb-3
                flex flex-col items-center justify-center">
        <template v-for="value in SiteConfig.icp" v-if="SiteConfig.icp">
            <a :href="value.url" target="_blank" class="text-sm text-gray-700 hover:text-gray-900 transition-colors duration-300">{{ value.name }}</a>
        </template>
        <p class="text-sm text-gray-700" v-if="SiteConfig.right">&copy; {{ SiteConfig.right }}</p>
    </footer>
</template>

<script setup lang="ts">
import { Icon } from '@iconify/vue'
import AuthorInfo from '../configs/author.json';
import SiteConfig from '../configs/site.json';
</script>