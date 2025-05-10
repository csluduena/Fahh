<script setup lang="ts">
import { onMounted, ref } from 'vue'

const props = defineProps({
  channel: {
    type: String,
    default: 'fahhkies'
  },
  width: {
    type: String,
    default: '100%'
  },
  height: {
    type: String,
    default: '400'
  }
})

const twitchContainer = ref(null)
const hasLoaded = ref(false)

onMounted(() => {
  // Load the Twitch embed API
  const script = document.createElement('script')
  script.src = 'https://embed.twitch.tv/embed/v1.js'
  script.async = true
  script.onload = initializeTwitchEmbed
  document.body.appendChild(script)
})

function initializeTwitchEmbed() {
  if (!window.Twitch) {
    console.error('Twitch embed API not loaded')
    return
  }
  
  new window.Twitch.Embed(twitchContainer.value, {
    width: props.width,
    height: props.height,
    channel: props.channel,
    layout: 'video',
    autoplay: false,
    parent: ["localhost", "stackblitz.com"]
  })
  
  hasLoaded.value = true
}
</script>

<template>
  <div>
    <div ref="twitchContainer" class="tw-embed rounded-lg overflow-hidden shadow-xl"></div>
    <div v-if="!hasLoaded" class="flex h-full w-full items-center justify-center p-10 bg-gray-800 rounded-lg">
      <div class="text-center text-purple-300">
        <div class="animate-spin rounded-full h-12 w-12 border-4 border-purple-500 border-t-transparent mx-auto mb-4"></div>
        <p>Loading Twitch channel: {{ channel }}</p>
      </div>
    </div>
  </div>
</template>