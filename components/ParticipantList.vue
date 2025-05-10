<script setup lang="ts">
import { ref } from 'vue'

// Mock data - in a real scenario, this would be real user data
const participants = ref([
  { name: 'TwitchUser123', tier: 'VIP', months: 18 },
  { name: 'GameMaster42', tier: 'Subscriber', months: 12 },
  { name: 'StreamLover99', tier: 'Subscriber', months: 10 },
  { name: 'PurpleFan22', tier: 'Moderator', months: 24 },
  { name: 'ViewerPro', tier: 'Subscriber', months: 6 },
  { name: 'ChatterBox', tier: 'VIP', months: 15 },
  { name: 'TwitchAddict', tier: 'Subscriber', months: 8 },
  { name: 'LoyalFan', tier: 'Subscriber', months: 9 },
  { name: 'MemeQueen', tier: 'Moderator', months: 20 },
  { name: 'GameEnthusiast', tier: 'VIP', months: 14 }
])

// Determine CSS class based on tier
const getTierClass = (tier) => {
  switch(tier) {
    case 'VIP': return 'bg-purple-600'
    case 'Moderator': return 'bg-blue-600'
    case 'Subscriber': return 'bg-green-600'
    default: return 'bg-gray-600'
  }
}
</script>

<template>
  <div class="w-full max-w-4xl mx-auto">
    <h2 class="text-3xl font-bold mb-6 text-center text-purple-300">Event Participants</h2>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <div 
        v-for="(participant, idx) in participants" 
        :key="idx"
        class="p-4 rounded-lg shadow-lg border border-gray-700 backdrop-blur-sm bg-gray-900/50 transition-all duration-300 hover:transform hover:scale-105"
        v-motion
        :initial="{ y: 20, opacity: 0 }"
        :enter="{ y: 0, opacity: 1, transition: { delay: idx * 100 } }">
        
        <div class="flex items-center">
          <div class="w-10 h-10 rounded-full mr-3 flex items-center justify-center text-white font-bold" :class="getTierClass(participant.tier)">
            {{ participant.name.charAt(0) }}
          </div>
          
          <div>
            <div class="font-bold text-white">{{ participant.name }}</div>
            <div class="flex items-center text-sm">
              <span class="px-2 py-0.5 rounded-full text-xs mr-2" :class="getTierClass(participant.tier)">
                {{ participant.tier }}
              </span>
              <span class="text-gray-400">{{ participant.months }} months</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>