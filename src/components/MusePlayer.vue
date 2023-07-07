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
    if (!video || !player.value) return
    if (video === player.value.options.video) return
    player.value.setVideo(video)
  },
  {
    deep: true,
    immediate: true
  }
)

useScriptTag('https://muse.ai/static/js/embed-player.min.js', () => {
  player.value = (window as any).MusePlayer({
    container: '#muse-player',
    ...props.videoOptions
  })
})

const events = ['play', 'pause', 'seek', 'on', 'off', 'setVideo', 'setSpeed', 'setVolume']

defineExpose(
  events.reduce((events, event) => {
    return {
      ...events,
      [event]: (...args: any[]) => {
        player.value?.[event](...args)
      }
    }
  }, {} as any)
)
</script>

<template>
  <div id="muse-player"></div>
</template>
