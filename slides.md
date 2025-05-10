---
# Fahhkies Twitch Event
theme: seriph
background: https://i.imgur.com/VlFHG9l.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  ## Fahhkies Twitch Event
  Special presentation for Fahhkies stream event.
drawings:
  persist: false
css: unocss
---

# Holi Fahhkies owo

<div class="pt-12 flex justify-center">
  <img src="https://i.imgur.com/R57B6kp.gif?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2"/>
</div>

<div class="pt-12">
  <span @click="$slidev.nav.next" class="hover-button px-4 py-2 rounded cursor-pointer text-white">
    Tócame ésta 
    <img src="/public/img/THIS.gif" alt="THIS" style="display:inline; height:1.5em; vertical-align:middle;"/> 
    <i-carbon-arrow-right class="inline"/>
  </span>
</div>

<div class="audio-donut-container">
  <button id="audioDonutBtn" class="donut-btn vibrate-audio-btn">
    <span id="donutIcon" class="donut-icon">
      <svg id="playIcon" width="36" height="36" viewBox="0 0 36 36" style="display:inline;"><circle cx="18" cy="18" r="16" fill="none" stroke="#fff" stroke-width="8"/><polygon points="15,12 27,18 15,24" fill="#2196f3"/></svg>
      <svg id="pauseIcon" width="36" height="36" viewBox="0 0 36 36" style="display:none;"><circle cx="18" cy="18" r="16" fill="none" stroke="#fff" stroke-width="8"/><rect x="14" y="12" width="3.5" height="12" fill="#2196f3"/><rect x="20" y="12" width="3.5" height="12" fill="#2196f3"/></svg>
    </span>
  </button>
  <audio id="audioPlayer" src="/img/Gangplank Galleon Restored to HD.mp3"></audio>
</div>

<style>
.hover-button {
  background-color: #a970ff;
  transition: background-color 0.3s ease;
}
.hover-button:hover {
  background-color:rgb(113, 41, 236);
  transform: scale(1.3);
}
.audio-donut-container {
  position: absolute;
  right: 2.5rem;
  bottom: 2.5rem;
  z-index: 10;
}
.donut-btn {
  width: 70px;
  height: 70px;
  background: radial-gradient(circle at 60% 30%, #fff8, #a970ff 80%);
  border: 5px solid #a970ff;
  border-radius: 50%;
  box-shadow: 0 4px 16px #a970ff88, 0 0 0 8px #fff2 inset;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  transition: box-shadow 0.2s, transform 0.2s;
  cursor: pointer;
  outline: none;
}
.donut-btn:active {
  background: radial-gradient(circle at 60% 30%, #fff9, #7130ec 80%);
  box-shadow: 0 2px 8px #7130ec88, 0 0 0 8px #fff2 inset;
}
.donut-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}
.vibrate-audio-btn {
  animation: vibrate 0.3s infinite linear;
}
@keyframes vibrate {
  0% { transform: translate(0, 0); }
  20% { transform: translate(-1px, 1px); }
  40% { transform: translate(-1px, -1px); }
  60% { transform: translate(1px, 1px); }
  80% { transform: translate(1px, -1px); }
  100% { transform: translate(0, 0); }
}
.custom-img-bg .slidev-layout.image-right {
  background-size: 50% !important;
  background-repeat: no-repeat !important;
  background-position: right center !important;
}
</style>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  const video = document.getElementById('videoPlayer')
  if (video) {
    video.volume = 0.2 // 20%
  }
  // Audio player setup
  const audio = document.getElementById('audioPlayer')
  if (audio) {
    audio.volume = 0.15 // 15%
  }
  const donutBtn = document.getElementById('audioDonutBtn')
  const playIcon = document.getElementById('playIcon')
  const pauseIcon = document.getElementById('pauseIcon')
  if (donutBtn && audio && playIcon && pauseIcon) {
    donutBtn.onclick = () => {
      if (audio.paused) {
        audio.play()
        playIcon.style.display = 'none'
        pauseIcon.style.display = 'inline'
      } else {
        audio.pause()
        playIcon.style.display = 'inline'
        pauseIcon.style.display = 'none'
      }
    }
    audio.onended = () => {
      playIcon.style.display = 'inline'
      pauseIcon.style.display = 'none'
    }
    // Pausar audio al cambiar de slide
    window.addEventListener('slidev:navigate', () => {
      audio.pause()
      playIcon.style.display = 'inline'
      pauseIcon.style.display = 'none'
    })
  }
})
</script>

<!--
Introduction slide for Fahhkies' event
-->

---
layout: two-cols
---

# FahhKistan y los Kakiers
<div 
  v-motion
  :initial="{ x: -80, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 200, duration: 1000 } }">

Holi, esto comenzó como un meme, para knowPots y fue creciendo de a poquito (Como la tuya). 

Hasta que decidí hacer un ad de KnowPots y pedí ayuda a varios fahhkiers.

- Hasta entonces he pagado € 1600 Entre todos los participantes (Solo me cobró uno y fue Jazzvier)

  <div 
    v-motion
    :initial="{ scale: 0.8, opacity: 0 }"
    :enter="{ scale: 1, opacity: 1, transition: { delay: 600, duration: 800 } }"
    class="w-72 h-48  rounded-lg shadow-xl flex items-center justify-center text-white">
    <img src="/img/99eebfb86.png" alt="99eebfb86" style="max-height: 100%; max-width: 100%; object-fit: contain;"/>
  </div>

</div>

::right::

<div class="pl-4 h-full flex flex-col justify-center items-center">
<div class="pl-4 h-full flex flex-col justify-center items-center">
  <video
    id="videoPlayer"
    src="/img/knowpots.mp4"
    controls
    autoplay
    style="max-height: 100%; max-width: 100%; object-fit: contain;"
    class="w-full h-full rounded-lg shadow-xl">
  </video>
</div>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  const video = document.getElementById('videoPlayer')
  if (video) {
    video.volume = 0.2 // 20%
  }
})
</script>
  
  <div 
    v-motion
    :initial="{ scale: 0.8, opacity: 0 }"
    :enter="{ scale: 1, opacity: 1, transition: { delay: 600, duration: 800 } }"
    class="w-72 h-48  rounded-lg shadow-xl flex items-center justify-center text-white">
    <img src="/img/fahhmilia.png" alt="99eebfb86" style="max-height: 100%; max-width: 100%; object-fit: contain;"/>
  </div>
</div>


---
layout: center
background: https://i.imgur.com/znAXbtS.png
class: 'bg-cover bg-center'
---



#

<!-- Fondo de pantalla completo -->
<div class="absolute top-0 left-0 w-full h-full -z-10">
  <img src="https://i.imgur.com/LlrLrce.png" alt="Fondo oscuro" class="w-full h-full object-cover" />
</div>

<!-- Contenido centrado encima del fondo -->
<div class="flex flex-col items-center pt-8 text-white relative z-10">
  <div>
    <iframe width="560" height="315" 
    src="https://www.youtube.com/embed/_ZvknalXsfg?modestbranding=1&rel=0&controls=1" 
    title="YouTube video player" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
</iframe> 
  </div>

  <h1 class="text-3xl my-4">Besito owo!</h1>

  <img src="/img/image.png" alt="Fahhkies corazón" style="height: 80px;" class="mb-6"/>

  <div class="absolute bottom-10 right-10 text-sm opacity-70">
    Creado con 💜 para Fahhkies
  </div>
</div>
