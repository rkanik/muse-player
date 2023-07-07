<script lang="ts" setup>
import { ref, watch } from 'vue'
import { useScriptTag } from '@vueuse/core'

const props = defineProps<{
  videoOptions: {
    video: string
    [key: string]: any
  }
}>()

const player = ref()

watch(
  () => props.videoOptions.video,
  (video) => {
    if (!player.value) return
    if (video === player.value.options.video) return
    player.value.setVideo(video)
  },
  {
    deep: true,
    immediate: true
  }
)

useScriptTag('https://muse.ai/static/js/embed-player.min.js', () => {
  player.value = window.MusePlayer({
    container: '#muse-player',
    ...props.videoOptions
  })
})
</script>

<template>
  <div id="muse-player"></div>
</template>
