<template>
  <nav class="Titlebar">
    <!-- menu -->
    <div
      class="Icon-wrapper Icon-wrapper--titlebar Icon-wrapper--double--right"
      style="position: absolute; top: 48px; right: 85px;"
      @click="toggleDrawer"
    >
    <img src="../assets/list_white.png">
    </div>

    <div
      class="Icon-wrapper Icon-wrapper--titlebar Icon-wrapper--double--right"
      style="position: absolute; top: 132px; right: 85px;"
      @click="toggleDrawer"
    >
    <img src="../assets/chart_white.png">
    </div>

    <div
      class="Icon-wrapper Icon-wrapper--titlebar Icon-wrapper--double--right"
      style="position: absolute; top: 216px; right: 85px;"
      @click="toggleDrawer"
    >
    <img src="../assets/music_white.png">
    </div>
  </nav>
</template>

<script>
// import { ipcRenderer } from 'electron'

export default {
  computed: {
    drawerOpen() {
      return this.$store.getters.drawerOpen
    }
  },

  methods: {
    toggleDrawer() {
      this.$store.dispatch('toggleDrawer')
    },
    toggleChart() {
      this.$store.dispatch('toggleDrawer1')
    },
    toggleMusic() {
      this.$store.dispatch('toggleDrawer')
    }
  }
}
</script>

<style lang="scss" scoped>
.Menu-line {
  background-color: $colorBlueGrey;
  display: inline-block;
  transition: $transitionDefault;
  width: 100px;
  height: 300px;
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

.Icon-wrapper:hover {
  padding: 16px;
  background: lightgray;
}
</style>
