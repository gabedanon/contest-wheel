<template>
  <div class="wheel" :class="spinning ? 'spinning' : ''">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 294.6 313.6"><path fill="#fff" d="M143.6 218.4v87.8c-32.8-.8-62.9-12.2-87.2-30.8 17.5-15.1 31.6-34 41-55.4-2.8.2-5.6.4-8.3.6-9.1 19.3-22.4 36.4-38.6 50.1-13.1-11.2-24.3-24.5-32.9-39.6-2.5.6-5 1.3-7.3 1.9 26.8 48 78.1 80.5 137 80.5s110.2-32.5 137-80.5c-2.3-.7-4.8-1.3-7.3-1.9-8.6 15-19.8 28.4-32.9 39.6-16.2-13.7-29.5-30.8-38.7-50.2-2.7-.2-5.5-.4-8.3-.6 9.4 21.4 23.5 40.3 41 55.4-24.3 18.6-54.4 30-87.2 30.8v-87.8h-3.6c-1.2.1-2.5.1-3.7.1zM147.3 0C79.7 0 22 42.9 0 102.9h7.8c9.1-23.5 23.9-44.1 42.8-60.1 18.9 16 33.7 36.6 42.8 60.1h7.8C92 77.6 76.4 55.4 56.4 38.2c24.3-18.6 54.5-30 87.3-30.8v95.5h7.3V7.4c32.8.8 63 12.1 87.3 30.8-20 17.3-35.6 39.5-44.9 64.7h7.7c9.1-23.5 24-44 42.8-60.1 18.9 16 33.7 36.6 42.8 60.1h7.8C272.6 42.9 214.9 0 147.3 0z"/></svg>
    <div class="text" @click="spin">{{ winner ? winner : 'Spin' }}</div>
  </div>
</template>

<script>
import entries from '../entries'
import { sample } from 'lodash'

export default {
  name: 'TheWheel',
  data: () => ({
    spinning: false,
    entries,
    winner: null
  }),
  methods: {
    selectWinner () {
      this.winner = sample(this.entries)
      this.entries.splice(this.entries.indexOf(this.winner), 1)
    },
    spin () {
      const audio = new Audio('https://cdn.dunk.town/audio/wheel.mp3')
      audio.play()
      this.spinning = true
      window.setTimeout(() => {
        this.selectWinner()
      }, 1500)
      window.setTimeout(() => {
        this.spinning = false
      }, 3000)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wheel {
  height: 90vh;
  position: relative;
}

.wheel svg {
  width: auto;
  height: 100%;
  display: block;
}

.wheel .text {
  position: absolute;
  color: #fff;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 16vh;
  width: 100vw;
  text-align: center;
  text-transform: uppercase;
  font-family: 'Oswald', sans-serif;
  cursor: default;
}

.wheel.spinning .text {
  opacity: 0;
}

.wheel.spinning svg {
  animation-name: spin;
  animation-duration: 3s;
  animation-timing-function: ease-out;
  animation-fill-mode: both;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(1800deg);
  }
}
</style>
