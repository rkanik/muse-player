<script setup lang="ts">
import MusePlayer from '@/components/MusePlayer.vue'
import { reactive } from 'vue'

const videos = ['y8zH87z', 'DjJZiTn', 'hRkdqPR', 'XmWryKL']

const videoOptions = reactive({
  video: 'XmWryKL',
  loop: true,
  width: '100%',
  height: '100%',
  sizing: 'fill',
  autoplay: true
})
</script>

<template>
  <main class="h-screen flex flex-col items-center bg-gray-800 py-16">
    <div class="max-w-3xl w-full">
      <input
        v-model="videoOptions.video"
        type="text"
        placeholder="Enter video id here..."
        class="w-full bg-gray-700 py-2 px-4 rounded focus:outline-none text-white"
      />

      <div class="flex space-x-2 mt-1">
        <button
          v-for="video in videos"
          :key="video"
          class="text-sm text-gray-400 hover:text-white underline"
          @click="videoOptions.video = video"
        >
          {{ video }}
        </button>
      </div>

      <MusePlayer
        :video-options="videoOptions"
        class="mt-2 rounded overflow-hidden h-[432px] bg-black"
      />
    </div>
  </main>
</template>
