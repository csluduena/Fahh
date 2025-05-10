---
# Fahhkies Twitch Event - Advanced Version
theme: seriph
background: '#18181B'
class: 'slide-bg-twitch'
highlighter: shiki
lineNumbers: false
info: |
  ## Fahhkies Twitch Special Event
  Interactive presentation with animations, videos, and community showcase.
drawings:
  persist: false
css: 
  - unocss
  - ./styles/custom.css
---

# <span class="text-purple-400">Fahhkies</span> Twitch Event

<div class="pt-8 flex justify-center">
  <img src="https://images.pexels.com/photos/2261166/pexels-photo-2261166.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="w-64 h-64 rounded-full border-4 border-purple-500 shadow-xl glow float-animation" />
</div>

<div class="pt-12">
  <span @click="$slidev.nav.next" class="twitch-button">
    Let's Begin <i-carbon-arrow-right class="inline"/>
  </span>
</div>

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>

<!--
Welcome to the special Fahhkies Twitch event presentation
-->

---
layout: two-cols
background: '#18181B'
class: 'slide-bg-twitch'
---

# <span class="text-purple-400">About</span> Fahhkies

<div 
  v-motion
  :initial="{ x: -80, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 200, duration: 1000 } }">

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum auctor magna vel nunc finibus, at dapibus nisi pulvinar.

<div class="space-y-2 mt-4">
  <div class="flex items-center">
    <i-carbon-checkmark-filled class="text-purple-400 mr-2" /> Twitch Partner since 2021
  </div>
  <div class="flex items-center">
    <i-carbon-checkmark-filled class="text-purple-400 mr-2" /> Known for amazing gameplay and community
  </div>
  <div class="flex items-center">
    <i-carbon-checkmark-filled class="text-purple-400 mr-2" /> Weekly events and special streams
  </div>
  <div class="flex items-center">
    <i-carbon-checkmark-filled class="text-purple-400 mr-2" /> Dedicated community of viewers
  </div>
</div>

</div>

::right::

<div class="pl-4 h-full flex flex-col justify-center items-center">
  <div 
    v-motion
    :initial="{ y: 50, opacity: 0 }"
    :enter="{ y: 0, opacity: 1, transition: { delay: 300, duration: 800 } }"
    class="twitch-card w-full h-48 mb-4 flex items-center justify-center">
    <div class="text-center">
      <i-carbon-game-console class="text-4xl text-purple-400 mb-2" />
      <div class="text-white">Gaming Excellence</div>
    </div>
  </div>
  
  <div 
    v-motion
    :initial="{ y: 50, opacity: 0 }"
    :enter="{ y: 0, opacity: 1, transition: { delay: 600, duration: 800 } }"
    class="twitch-card w-full h-48 flex items-center justify-center">
    <div class="text-center">
      <i-carbon-group class="text-4xl text-purple-400 mb-2" />
      <div class="text-white">Amazing Community</div>
    </div>
  </div>
</div>

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>

---
layout: center
background: '#18181B'
class: 'text-center slide-bg-twitch'
---

# <span class="text-purple-400">Watch</span> Fahhkies Live

<div class="my-10">
  <TwitchEmbed channel="fahhkies" height="400" />
</div>

<div class="text-sm text-gray-400">
  Follow at <a href="https://www.twitch.tv/fahhkies" target="_blank" class="text-purple-400 hover:text-purple-300">twitch.tv/fahhkies</a>
</div>

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>

---
layout: center
background: '#18181B'
class: 'text-center slide-bg-twitch'
---

# <span class="text-purple-400">Featured</span> Video

<div 
  v-motion
  :initial="{ scale: 0.8, opacity: 0 }"
  :enter="{ scale: 1, opacity: 1 }">
  <Youtube id="dQw4w9WgXcQ" />
</div>

<div class="pt-4 text-sm text-gray-400">
  Check out more content at <a href="https://www.twitch.tv/fahhkies" target="_blank" class="text-purple-400 hover:text-purple-300">twitch.tv/fahhkies</a>
</div>

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>

---
layout: center
background: '#18181B'
class: 'slide-bg-twitch'
---

# <span class="text-purple-400">Our</span> Amazing Community

<ParticipantList />

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>

---
layout: center
background: '#18181B'
class: 'text-center slide-bg-twitch'
---

# <span class="text-purple-400">Thank</span> You!

<div class="text-xl text-gray-400 mt-4 mb-8">
  Follow Fahhkies for more amazing content
</div>

<div class="flex justify-center space-x-6">
  <a href="https://www.twitch.tv/fahhkies" target="_blank" class="twitch-button flex items-center">
    <i-carbon-logo-twitch class="mr-2 text-2xl" /> Twitch
  </a>
  <a href="#" class="twitch-button flex items-center" style="background-color: #FF0000">
    <i-carbon-logo-youtube class="mr-2 text-2xl" /> YouTube
  </a>
  <a href="#" class="twitch-button flex items-center" style="background-color: #1DA1F2">
    <i-carbon-logo-twitter class="mr-2 text-2xl" /> Twitter
  </a>
</div>

<div class="absolute bottom-10 right-10">
  <div class="text-sm opacity-50">Created with 💜 for Fahhkies</div>
</div>

<div class="gradient-mesh absolute top-0 left-0 right-0 bottom-0 opacity-20 z-[-1]"></div>