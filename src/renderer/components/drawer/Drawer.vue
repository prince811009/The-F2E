<template>
  <div class="Drawer">
  <div class="timeMissionWrap">
    <app-Timer-Mission />
  </div>
    <transition
      name="fade"
      mode="out-in"
    >
      <component :is="currentDrawer" />
    </transition>
    <app-drawer-menu />
    <div class="titleBar"><app-titlebar /></div>
    <div class="closeWin"
    @click="toggleDrawer"
    >
      <img src="../../assets/close_white.png"
      @click="toggleDrawer"
      >
    </div>
  </div>
</template>

<script>
import appDrawerTimer from '@/components/drawer/Drawer-timer'
import appTimerMission from '@/components/timer/Timer-mission'
import appTitlebar from '@/components/Titlebar'

export default {
  name: 'Drawer',

  components: {
    appDrawerTimer,
    appTimerMission,
    appTitlebar
  },

  computed: {
    currentDrawer() {
      return this.$store.getters.currentDrawer
    }
  },
  methods: {
    toggleDrawer() {
      this.$store.dispatch('toggleDrawer')
    }
  }
}
</script>

<style lang="scss" scoped>
.Drawer {
  background-color: #003164;
  position: relative;
  width: 100%;
  min-height: 100%;
  margin-top: -68px;
  padding: 45px 0px;
  z-index: 21;
  -webkit-app-region: no-drag;
}

.timeMissionWrap {
  width: 445px;
  position: absolute;
  top: 48px;
  left: 560px;
}

.titleBar {
  position:absolute;
  top: 48px;
  left: 200px;
}

.closeWin {
  width: 48px;
  height: 48px;
  position: absolute;
  top:48px;
  right: 85px;
}
</style>
