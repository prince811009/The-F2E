<template>
  <section class="Container Footer">
    <div class="Round-wrapper TextButton"
        @click="callForReset">
    </div>
  </section>
</template>

<script>
import { EventBus } from '@/utils/event-bus'

export default {
  name: 'TimerFooter',
  data() {
    return {
      currentMousePosition: {
        x: null,
        y: null
      },
      localVolume: 0,
      volumeSliderHidden: true
    }
  },
  computed: {
    // store getters
    currentRound() {
      return this.$store.getters.currentRound
    },

    round() {
      return this.$store.getters.round
    },

    workRounds() {
      return this.$store.getters.workRounds
    },

    volume() {
      return this.$store.getters.volume
    }
  },

  methods: {
    callForReset() {
      EventBus.$emit('call-timer-reset')
    },

    /**
     * Hides the volume slider unless the last recorded mouse position
     * falls within a range containing the volume slider.
     */
    volumeSliderTimeout() {
      setInterval(() => {
        if (
          this.currentMousePosition.x >= 305 &&
          this.currentMousePosition.x <= 355 &&
          (this.currentMousePosition.y >= 305 &&
            this.currentMousePosition.y <= 455)
        ) {
        } else {
          this.volumeSliderHidden = true
        }
      }, 6000)
    },

    skipRound() {
      EventBus.$emit('timer-completed')
    },

    toggleMute() {
      // set volume to zero if not muted
      // otherwise set to 100 (default)
      if (this.localVolume === '0') {
        this.localVolume = '100'
        this.$store.dispatch('setVolume', 100)
      } else {
        this.localVolume = '0'
        this.$store.dispatch('setVolume', 0)
      }
    },

    setVolume(e) {
      this.$store.dispatch('setVolume', parseInt(e.target.value))
    }
  },

  mounted() {
    this.localVolume = this.volume
    this.volumeSliderTimeout()

    // record last mouse position for volume slider timeout
    window.addEventListener('mousemove', e => {
      this.currentMousePosition.x = e.clientX
      this.currentMousePosition.y = e.clientY
    })
  }
}
</script>

<style lang="scss" scoped>
.Footer {
  align-items: center;
  display: flex;
  justify-content: space-between;
}

.Round-wrapper {
  text-align: center;
  width: 16px;
  height: 16px;
  background: white;
  position: absolute;
  top: 52%;
  left: 70%;
  z-index: 20;
}

.Slider-wrapper {
  padding: 8px;
  position: absolute;
  top: -61px;
  right: -29px;
}

.Slider {
  &::-webkit-slider-runnable-track {
    background-color: $colorBlueGrey;
  }
  &::-webkit-slider-thumb {
    margin-top: -7px;
    transition: $transitionDefault;
    &:hover {
      background-color: $colorRed;
      border-color: $colorRed;
    }
  }
}
</style>
