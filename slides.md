---
# Fahhkies Twitch Event
theme: seriph
colorSchema: 'dark'
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

<!-- Importar Font Awesome para los iconos del clima -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

# Holi Fahhkies owo

<!-- Horario Perú/Bolivia en la esquina superior izquierda -->
<div class="fixed top-4 left-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <img src="/img/pe.png" alt="País" id="bandera-pais" style="height: 1.5em; cursor: pointer;"/>
  <span id="hora-pais">05:48:40 p. m.</span>
</div>

<!-- Clima de Lima/La Paz en la esquina superior derecha -->
<div class="fixed top-4 right-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <span id="clima-ciudad"><i class="fas fa-sun"></i> 24°C</span>
  <span id="nombre-ciudad">Lima, PE</span>
</div>

<!-- Flecha izquierda -->
<button class="fixed left-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.prev">
  <img src="/img/left1.png" alt="Anterior" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>

<!-- Flecha derecha -->
<button class="fixed right-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.next">
  <img src="/img/right1.png" alt="Siguiente" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>


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
      <svg id="playIcon" width="110" height="110" viewBox="0 0 36 36" style="display:inline;">
        <polygon points="15,12 27,18 15,24" fill="#fff"/>
      </svg>
      <svg id="pauseIcon" width="110" height="110" viewBox="0 0 36 36" style="display:none;">
        <rect x="14" y="12" width="3.5" height="12" fill="#fff"/>
        <rect x="20" y="12" width="3.5" height="12" fill="#fff"/>
      </svg>
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
  width: 100px;
  height: 100px;
  background: url('/img/d.png') center center / cover no-repeat;
  border: none;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  transition: box-shadow 0.2s, transform 0.2s;
  cursor: pointer;
  outline: none;
  box-shadow: 0 4px 16px #a970ff88;
}
.donut-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  left: 46%;
  top: 52%;
  transform: translate(-50%, -50%);
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
import { onMounted, ref } from 'vue'

// Variable reactiva para el país actual
const paisActual = ref('peru')

// Función para cambiar entre países
function cambiarPais() {
  console.log('Cambiando país de', paisActual.value, 'a', paisActual.value === 'peru' ? 'bolivia' : 'peru')
  
  if (paisActual.value === 'peru') {
    paisActual.value = 'bolivia'
    // Cambiar todas las banderas
    const banderas = document.querySelectorAll('#bandera-pais')
    banderas.forEach(bandera => {
      bandera.src = '/img/bol.png'
      bandera.alt = 'Bolivia'
    })
    // Cambiar nombres de ciudad
    const nombresCiudad = document.querySelectorAll('#nombre-ciudad')
    nombresCiudad.forEach(nombre => {
      nombre.textContent = 'La Paz, BO'
    })
  } else {
    paisActual.value = 'peru'
    // Cambiar todas las banderas
    const banderas = document.querySelectorAll('#bandera-pais')
    banderas.forEach(bandera => {
      bandera.src = '/img/pe.png'
      bandera.alt = 'Perú'
    })
    // Cambiar nombres de ciudad
    const nombresCiudad = document.querySelectorAll('#nombre-ciudad')
    nombresCiudad.forEach(nombre => {
      nombre.textContent = 'Lima, PE'
    })
  }
  
  // Actualizar inmediatamente hora y clima
  actualizarHoraPais()
  actualizarClimaCiudad()
}

// Variables globales para las funciones
let actualizarHoraPais
let actualizarClimaCiudad
let intervalHora
let intervalClima
let currentSlide = 0

onMounted(() => {
  // Audio donut
  const audio = document.getElementById('audioPlayer')
  const donutBtn = document.getElementById('audioDonutBtn')
  const playIcon = document.getElementById('playIcon')
  const pauseIcon = document.getElementById('pauseIcon')
  if (audio) {
    audio.volume = 0.15 // 15%
  }
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

  // Video del slide 2
  const video = document.getElementById('videoPlayer')
  if (video) {
    video.volume = 0.2
    window.addEventListener('slidev:navigate', () => {
      video.pause()
    })
  }
   
  // Actualizar hora según el país seleccionado
  actualizarHoraPais = function() {
    const horaElements = document.querySelectorAll('#hora-pais')
    const timeZone = paisActual.value === 'peru' ? 'America/Lima' : 'America/La_Paz'
    const options = { 
      hour: '2-digit', 
      minute: '2-digit', 
      second: '2-digit', 
      hour12: true,
      timeZone: timeZone
    }
    const horaActual = new Date().toLocaleTimeString('es', options)
    
    horaElements.forEach(el => {
      if (el) {
        el.textContent = horaActual
      }
    })
  }
   
  // Obtener icono según el código del clima
  function getWeatherIcon(iconCode) {
    const iconMap = {
      '01d': '<i class="fas fa-sun"></i>',
      '01n': '<i class="fas fa-moon"></i>',
      '02d': '<i class="fas fa-cloud-sun"></i>',
      '02n': '<i class="fas fa-cloud-moon"></i>',
      '03d': '<i class="fas fa-cloud"></i>',
      '03n': '<i class="fas fa-cloud"></i>',
      '04d': '<i class="fas fa-cloud"></i>',
      '04n': '<i class="fas fa-cloud"></i>',
      '09d': '<i class="fas fa-cloud-showers-heavy"></i>',
      '09n': '<i class="fas fa-cloud-showers-heavy"></i>',
      '10d': '<i class="fas fa-cloud-rain"></i>',
      '10n': '<i class="fas fa-cloud-rain"></i>',
      '11d': '<i class="fas fa-bolt"></i>',
      '11n': '<i class="fas fa-bolt"></i>',
      '13d': '<i class="fas fa-snowflake"></i>',
      '13n': '<i class="fas fa-snowflake"></i>',
      '50d': '<i class="fas fa-smog"></i>',
      '50n': '<i class="fas fa-smog"></i>'
    }
    return iconMap[iconCode] || '<i class="fas fa-sun"></i>'
  }
  
  // Actualizar clima según la ciudad seleccionada
  actualizarClimaCiudad = function() {
    const climaElements = document.querySelectorAll('#clima-ciudad')
    if (climaElements.length > 0) {
      // Valores predeterminados según el país
      const defaultData = {
        peru: {
          temp: 24,
          icon: '<i class="fas fa-sun"></i>'
        },
        bolivia: {
          temp: 15,
          icon: '<i class="fas fa-cloud"></i>'
        }
      }
      
      // Mostrar datos predeterminados inmediatamente mientras se carga la API
      const defaultCountry = paisActual.value
      climaElements.forEach(el => {
        el.innerHTML = `${defaultData[defaultCountry].icon} ${defaultData[defaultCountry].temp}°C`
      })
      
      // Intentar obtener datos reales
      try {
        const apiKey = 'DEMO_KEY'
        const ciudad = paisActual.value === 'peru' ? 'Lima,pe' : 'La Paz,bo'
        
        fetch(`https://api.openweathermap.org/data/2.5/weather?q=${ciudad}&units=metric&appid=${apiKey}`)
          .then(response => {
            if (!response.ok) {
              throw new Error('Error en la respuesta de la API')
            }
            return response.json()
          })
          .then(data => {
            const temp = Math.round(data.main.temp)
            const icon = getWeatherIcon(data.weather[0].icon)
            
            // Actualizar todos los elementos de clima
            climaElements.forEach(el => {
              el.innerHTML = `${icon} ${temp}°C`
            })
          })
          .catch(error => {
            console.log('Error al obtener el clima:', error)
            // Ya mostramos los datos predeterminados, así que no hacemos nada más
          })
      } catch (error) {
        console.log('Error al intentar obtener el clima:', error)
        // Ya mostramos los datos predeterminados, así que no hacemos nada más
      }
    }
  }
  
  // Limpiar intervalos anteriores si existen
  if (intervalHora) clearInterval(intervalHora)
  if (intervalClima) clearInterval(intervalClima)
  
  // Configurar nuevos intervalos
  actualizarHoraPais() // Actualizar hora inmediatamente
  intervalHora = setInterval(actualizarHoraPais, 1000) // Actualizar cada segundo
  
  actualizarClimaCiudad() // Actualizar clima inmediatamente
  intervalClima = setInterval(actualizarClimaCiudad, 600000) // Actualizar cada 10 minutos
  
  // Configurar evento de clic para todas las banderas
  function configurarEventosBanderas() {
    const banderas = document.querySelectorAll('#bandera-pais')
    
    // Eliminar eventos anteriores para evitar duplicados
    banderas.forEach(bandera => {
      // Clonar y reemplazar para eliminar todos los listeners anteriores
      const nuevaBandera = bandera.cloneNode(true)
      if (bandera.parentNode) {
        bandera.parentNode.replaceChild(nuevaBandera, bandera)
      }
      
      // Agregar el nuevo evento de clic
      nuevaBandera.addEventListener('click', function(e) {
        e.preventDefault()
        e.stopPropagation()
        cambiarPais()
      }, true)
    })
    
    console.log(`Configurados eventos en ${banderas.length} banderas`)
  }
  
  // Configurar eventos inicialmente
  configurarEventosBanderas()
  
  // Función específica para manejar el slide 3
  function manejarSlide3() {
    // Asegurarse de que estamos en el slide 3
    if (currentSlide === 2) {
      console.log('Estamos en el slide 3, configurando eventos especiales')
      
      // Configurar eventos directamente en la bandera del slide 3
      const banderaSlide3 = document.querySelector('.slidev-page-3 #bandera-pais')
      if (banderaSlide3) {
        console.log('Bandera del slide 3 encontrada, configurando evento')
        banderaSlide3.onclick = null // Eliminar eventos anteriores
        banderaSlide3.addEventListener('click', function(e) {
          e.preventDefault()
          e.stopPropagation()
          console.log('Clic en bandera del slide 3')
          cambiarPais()
        }, true)
      }
    }
  }
  
  // Reconfigurar eventos después de cambiar de slide
  window.addEventListener('slidev:navigate', (event) => {
    console.log('Navegación detectada, reconfigurando eventos...')
    
    // Actualizar el número de slide actual
    if (event && event.detail) {
      currentSlide = event.detail.index
      console.log('Navegando al slide:', currentSlide + 1)
    }
    
    // Dar tiempo para que el DOM se actualice
    setTimeout(() => {
      configurarEventosBanderas()
      actualizarHoraPais()
      actualizarClimaCiudad()
      manejarSlide3() // Manejar específicamente el slide 3
    }, 300) // Aumentado a 300ms para dar más tiempo
  })
  
  // Configurar eventos para el slide inicial
  setTimeout(() => {
    manejarSlide3()
  }, 500)
})
</script>

<!--
Introduction slide for Fahhkies' event
-->

---
layout: two-cols
---
#
#
# FahhKistan y los Kakiers

<!-- Horario Perú/Bolivia en la esquina superior izquierda -->
<div class="fixed top-4 left-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <img src="/img/pe.png" alt="País" id="bandera-pais" style="height: 1.5em; cursor: pointer;"/>
  <span id="hora-pais">05:48:40 p. m.</span>
</div>

<!-- Clima de Lima/La Paz en la esquina superior derecha -->
<div class="fixed top-4 right-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <span id="clima-ciudad"><i class="fas fa-sun"></i> 24°C</span>
  <span id="nombre-ciudad">Lima, PE</span>
</div>

<!-- Flecha izquierda -->
<button class="fixed left-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.prev">
  <img src="/img/left1.png" alt="Anterior" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>

<!-- Flecha derecha -->
<button class="fixed right-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.next">
  <img src="/img/right1.png" alt="Siguiente" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>


<div 
  v-motion
  :initial="{ x: -80, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 200, duration: 1000 } }">

Holi, esto comenzó como un meme, para knowPots y fue creciendo de a poquito (como la tuya). 

Hasta que decidí hacer un ad de KnowPots y pedí ayuda a varios fahhkiers.

- Hasta entonces he pagado 1600€, entre todos los participantes (solo me cobró una y fue AbrilNW)

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

<!-- Horario Perú/Bolivia en la esquina superior izquierda -->
<div class="fixed top-4 left-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <img src="/img/pe.png" alt="País" id="bandera-pais" style="height: 1.5em; cursor: pointer;"/>
  <span id="hora-pais">05:48:40 p. m.</span>
</div>

<!-- Clima de Lima/La Paz en la esquina superior derecha -->
<div class="fixed top-4 right-4 z-50 bg-black/60 px-4 py-2 rounded text-white shadow flex items-center gap-2">
  <span id="clima-ciudad"><i class="fas fa-sun"></i> 24°C</span>
  <span id="nombre-ciudad">Lima, PE</span>
</div>

<!-- Flecha izquierda -->
<button class="fixed left-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.prev">
  <img src="/img/left1.png" alt="Anterior" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>

<!-- Flecha derecha -->
<button class="fixed right-4 top-1/2 -translate-y-1/2 z-50" @click="$slidev.nav.next">
  <img src="/img/right1.png" alt="Siguiente" class="w-17 h-10 transition-transform duration-200 hover:scale-150" />
</button>


<!-- Fondo de pantalla completo -->
<div class="absolute top-0 left-0 w-full h-full -z-10">
  <img src="https://i.imgur.com/LlrLrce.png" alt="Fondo oscuro" class="w-full h-full object-cover" />
</div>

<!-- Contenido centrado encima del fondo -->
<div class="flex flex-col items-center pt-8 text-white relative z-10">
  <div class="relative">
    <iframe width="560" height="315" 
    src="https://www.youtube.com/embed/_ZvknalXsfg?modestbranding=1&rel=0&controls=1" 
    title="YouTube video player" 
    frameborder="0"
    loading="lazy"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
    </iframe>
    <!-- Capa transparente para evitar que el iframe capture eventos -->
    <div class="absolute inset-0 pointer-events-none"></div>
  </div>

  <h1 class="text-3xl my-4">Besito owo!</h1>

  <img src="/img/image.png" alt="Fahhkies corazón" style="height: 80px;" class="mb-6"/>

  <div class="absolute bottom-10 right-10 text-sm opacity-70">
    Creado con 💜 para Fahhkies
  </div>
</div>
