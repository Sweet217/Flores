<template>
  <div class="flower-container">
    <div v-if="!isTimeUp" class="countdown-container">
      <h2 class="title">Flores Floreciendo El dia que las mas hermosa del mundo nacio, El</h2>
      <h3 class="subtitle">15 de Abril, 2025</h3>
      <div class="countdown">
        <div class="countdown-item">
          <span class="countdown-value">{{ timeLeft.days }}</span>
          <p class="countdown-label">Días</p>
        </div>
        <div class="countdown-item">
          <span class="countdown-value">{{ timeLeft.hours }}</span>
          <p class="countdown-label">Horas</p>
        </div>
        <div class="countdown-item">
          <span class="countdown-value">{{ timeLeft.minutes }}</span>
          <p class="countdown-label">Minutos</p>
        </div>
        <div class="countdown-item">
          <span class="countdown-value">{{ timeLeft.seconds }}</span>
          <p class="countdown-label">Segundos</p>
        </div>
      </div>
      <p class="message">Las flores se están preparando para florecer, y cada año te estaran esperando en el mismo lugar...</p>
    </div>
    
    <!-- Custom Image - Replace with your actual image path -->
    <div class="custom-image-container" :class="{ 'show-image': isTimeUp }">
      <img src="../assets/IMG_4555.JPG" alt="Birthday Image" class="custom-image" />
    </div>
    
    <div v-if="isTimeUp" class="bloomed-message">
      <h2>¡FELIZ CUMPLEAÑOS MI VIDA, MI AMOR, MI TODO</h2>
      <h3>No se hacer flores jASDJAJSD, te quiero <3 <span class="heart">❤️</span></h3>
    </div>

    <!-- Flowers Container -->
    <div class="flowers">
      <!-- Generate 21 flowers with v-for -->
      <div 
        v-for="(flower, index) in 21" 
        :key="index" 
        class="flower" 
        :class="{ 'bloom': isTimeUp }"
        :style="{
          left: `${(index % 7) * 14 + 5}%`, 
          bottom: `${Math.floor(index / 7) * 30}px`,
          transitionDelay: `${0.1 * index}s`,
          zIndex: index
        }"
      >
        <div class="flower-body">
          <!-- Petals -->
          <div 
            v-for="petalIndex in 8" 
            :key="`petal-${petalIndex}`"
            class="petal" 
            :class="`petal-${petalIndex} ${index % 3 === 0 ? 'pink' : index % 3 === 1 ? 'yellow' : 'mixed-' + (petalIndex % 2 === 0 ? 'pink' : 'yellow')}`"
          ></div>
          <!-- Center -->
          <div class="flower-center" :class="index % 3 === 0 ? 'yellow' : index % 3 === 1 ? 'pink' : 'yellow-dark'"></div>
        </div>
        <!-- Stem -->
        <div class="stem" :class="{ 'stem-tall': index % 4 === 0 }"></div>
        <!-- Leaves -->
        <div class="leaf leaf-left" :class="{ 'leaf-low': index % 2 === 0 }"></div>
        <div class="leaf leaf-right" :class="{ 'leaf-high': index % 3 === 0 }"></div>
      </div>
    </div>

    <!-- Falling Petals -->
    <div v-if="isTimeUp" class="falling-petals">
      <div 
        v-for="petal in 60" 
        :key="`falling-petal-${petal}`" 
        class="falling-petal" 
        :class="petal % 2 === 0 ? 'pink' : 'yellow'"
        :style="{
          left: `${Math.random() * 100}%`,
          animationDelay: `${Math.random() * 10}s`,
          animationDuration: `${Math.random() * 5 + 5}s`,
          transform: `scale(${Math.random() * 0.5 + 0.5}) rotate(${Math.random() * 360}deg)`,
          opacity: Math.random() * 0.7 + 0.3
        }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CumpleanosFlowers',
  data() {
    return {
      timeLeft: {
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0
      },
      isTimeUp: false,
      timer: null
    }
  },
  created() {
    this.calculateTimeLeft();
    this.timer = setInterval(this.calculateTimeLeft, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
  methods: {
    calculateTimeLeft() {
      const targetDate = new Date("April 14, 2025 00:00:00").getTime();
      const now = new Date().getTime();
      const difference = targetDate - now;
      
      if (difference > 0) {
        this.timeLeft = {
          days: Math.floor(difference / (1000 * 60 * 60 * 24)),
          hours: Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
          minutes: Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60)),
          seconds: Math.floor((difference % (1000 * 60)) / 1000)
        };
      } else {
        this.isTimeUp = true;
        this.timeLeft = { days: 0, hours: 0, minutes: 0, seconds: 0 };
        clearInterval(this.timer);
      }
    }
  }
}
</script>

<style scoped>
.flower-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #fdf6f9;
  padding: 1rem;
  font-family: 'Arial', sans-serif;
  position: relative;
  overflow: hidden;
}

.countdown-container {
  text-align: center;
  margin-bottom: 2rem;
  z-index: 100;
}

.title {
  font-size: 2rem;
  font-weight: bold;
  color: #ff6eb4;
  margin-bottom: 0.5rem;
  text-shadow: 1px 1px 3px rgba(0,0,0,0.1);
}

.subtitle {
  font-size: 1.5rem;
  font-weight: 600;
  color: #ff8cc6;
  margin-bottom: 1rem;
}

.countdown {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.countdown-item {
  background-color: white;
  padding: 0.75rem 1.25rem;
  border-radius: 1rem;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  min-width: 70px;
}

.countdown-value {
  font-size: 2rem;
  font-weight: bold;
  color: #ff80ab;
}

.countdown-label {
  font-size: 0.875rem;
  color: #666;
  margin: 0.25rem 0 0;
}

.message {
  margin-top: 1.5rem;
  color: #666;
  font-style: italic;
}

/* Custom Image Styling */
.custom-image-container {
  position: relative;
  width: 200px;
  height: 200px;
  margin: 0 auto;
  border-radius: 50%;
  overflow: hidden;
  border: 5px solid #ff80ab;
  box-shadow: 0 0 15px rgba(255, 128, 171, 0.5);
  opacity: 0;
  transform: scale(0);
  transition: all 1s ease-out;
  z-index: 150;
}

.custom-image-container.show-image {
  opacity: 1;
  transform: scale(1);
}

.custom-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.bloomed-message {
  text-align: center;
  margin: 2rem 0;
  animation: pulse 2s infinite alternate;
  z-index: 100;
}

.bloomed-message h2 {
  font-size: 2.5rem;
  font-weight: bold;
  color: #ff4081;
  margin-bottom: 0.5rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.15);
}

.bloomed-message h3 {
  font-size: 1.5rem;
  color: #ff80ab;
  font-weight: normal;
}

.heart {
  color: #ff4081;
  animation: beat 1s infinite alternate;
  display: inline-block;
}

/* Flowers */
.flowers {
  position: relative;
  width: 100%;
  max-width: 800px;
  height: 450px;
  margin-top: 20px;
}

.flower {
  position: absolute;
  transform: scale(0);
  transition: transform 1.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.flower.bloom {
  transform: scale(0.8);
}

.flower-body {
  position: relative;
  width: 30px;
  height: 30px;
  margin: 0 auto;
}

.petal {
  position: absolute;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}

.pink {
  background-color: #ff80ab;
}

.yellow {
  background-color: #ffeb3b;
}

.mixed-pink {
  background-color: #ff80ab;
}

.mixed-yellow {
  background-color: #ffeb3b;
}

.yellow-dark {
  background-color: #ffd600;
}

.petal-1 {
  left: 0;
  top: 0;
  transform: translate(-50%, -50%);
}

.petal-2 {
  right: 0;
  top: 0;
  transform: translate(50%, -50%);
}

.petal-3 {
  left: 0;
  bottom: 0;
  transform: translate(-50%, 50%);
}

.petal-4 {
  right: 0;
  bottom: 0;
  transform: translate(50%, 50%);
}

.petal-5 {
  left: 0;
  top: 50%;
  transform: translate(-75%, -50%);
}

.petal-6 {
  right: 0;
  top: 50%;
  transform: translate(75%, -50%);
}

.petal-7 {
  top: 0;
  left: 50%;
  transform: translate(-50%, -75%);
}

.petal-8 {
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 75%);
}

.flower-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 30px;
  height: 30px;
  border-radius: 50%;
  z-index: 10;
}

.stem {
  width: 4px;
  height: 80px;
  background-color: #4caf50;
  margin: -2px auto 0;
}

.stem-tall {
  height: 100px;
}

.leaf {
  position: absolute;
  width: 20px;
  height: 10px;
  background-color: #66bb6a;
  border-radius: 50%;
}

.leaf-left {
  bottom: 30px;
  left: -12px;
  transform: rotate(45deg);
}

.leaf-right {
  bottom: 45px;
  right: -12px;
  transform: rotate(-45deg);
}

.leaf-high {
  bottom: 60px;
}

.leaf-low {
  bottom: 25px;
}

/* Falling Petals */
.falling-petals {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.falling-petal {
  position: absolute;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  top: -20px;
  animation: falling linear forwards;
}

@keyframes falling {
  0% {
    top: -20px;
  }
  100% {
    top: 100%;
  }
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.05);
  }
}

@keyframes beat {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.3);
  }
}

/* Media Queries for Responsiveness */
@media (max-width: 768px) {
  .flowers {
    height: 350px;
  }
  
  .bloomed-message h2 {
    font-size: 1.8rem;
  }
  
  .bloomed-message h3 {
    font-size: 1.2rem;
  }
  
  .flower.bloom {
    transform: scale(0.6);
  }
  
  .custom-image-container {
    width: 150px;
    height: 150px;
  }
}

@media (max-width: 480px) {
  .countdown-item {
    padding: 0.5rem 0.75rem;
    min-width: 60px;
  }
  
  .countdown-value {
    font-size: 1.5rem;
  }
  
  .bloomed-message h2 {
    font-size: 1.5rem;
  }
  
  .flower.bloom {
    transform: scale(0.5);
  }
  
  .custom-image-container {
    width: 120px;
    height: 120px;
  }
}
</style>