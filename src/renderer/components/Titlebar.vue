<template>
  <nav class="Titlebar">
    <!-- menu -->
    <div
      class="Icon-wrapper Icon-wrapper--titlebar Icon-wrapper--single"
      style="position: absolute;"
      @click="toggleDrawer"
    >
      <div
        class="Menu-wrapper"
        :class="drawerOpen ? 'is-collapsed' : ''"
      >
        <div class="Menu-line"></div>
        <div class="Menu-line"></div>
      </div>
    </div>

    <h1 class="Title">Pomodoro</h1>

    <div
      class="Icon-group"
      style="position: absolute; top: 0; right: 0;"
    >
      <div
        class="Icon-wrapper Icon-wrapper--titlebar Icon-wrapper--double--left"
        style="padding-left: 18px"
        @click="winMinimize"
      >

      </div>
    </div>
  </nav>
</template>

<script>
import { ipcRenderer } from 'electron'

export default {
  computed: {
    drawerOpen() {
      return this.$store.getters.drawerOpen
    },

    minToTray() {
      return this.$store.getters.minToTray
    }
  },

  methods: {
    toggleDrawer() {
      this.$store.dispatch('toggleDrawer')
    },

    winClose() {
      ipcRenderer.send('window-close')
    },

    winMinimize() {
      ipcRenderer.send('window-minimize', this.minToTray)
    }
  }
}
</script>

<style lang="scss" scoped>
.Menu-line {
  background-color: $colorBlueGrey;
  display: inline-block;
  transition: $transitionDefault;
  width: 25px;
  height: 2px;
  &:last-child {
    width: 15px;
  }
}

.Menu-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 80%;
  &.is-collapsed {
    & .Menu-line:first-child {
      transform: rotate(-45deg);
      width: 12px;
    }
    & .Menu-line:last-child {
      transform: rotate(45deg);
      width: 12px;
    }
  }
}

.Title {
  color: #FF4384;
  font-size: 1rem;
  font-weight: 200;
  padding-top: 18px;
}

.Titlebar {
  letter-spacing: 0.05em;
  margin-bottom: 18px;
  position: relative;
  text-align: center;
  height: 50px;
  -webkit-app-region: drag;
}

.Icon-wrapper--titlebar {
  -webkit-app-region: no-drag;
  &:hover .Menu-line {
    background-color: $colorRed;
  }
  &:hover .Icon--close line,
  &:hover .Icon--minimize line {
    stroke: $colorRed;
  }
}
</style>
