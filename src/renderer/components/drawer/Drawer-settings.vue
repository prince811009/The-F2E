<template>
  <div class="Container">
    <p class="Drawer-heading"></p>
    <div class="Setting-wrapper">
      <div
        class="Checkbox"
        @click="isFinished"
        :class="isFinished ? 'is-active' : 'is-inactive'"
      ></div>
      <p class="Setting-title">THE FIRST THING TO DO TODAY</p>
    </div>
    <div class="Setting-wrapper">
      <div
        class="Checkbox"
        @click="isFinished"
        :class="isFinished ? 'is-active' : 'is-inactive'"
      ></div>
      <p class="Setting-title">THE SECOND THING TO DO TODAY</p>
    </div>
    <div class="Setting-wrapper">
      <div
        class="Checkbox"
        @click="isFinished"
        :class="isFinished ? 'is-active' : 'is-inactive'"
      ></div>
      <p class="Setting-title">THE THIRD THING TO DO TODAY</p>
    </div>
    <div class="Setting-wrapper">
      <div
        class="Checkbox"
        @click="isFinished"
        :class="isFinished ? 'is-active' : 'is-inactive'"
      ></div>
      <p class="Setting-title">THE THIRD THING TO DO TODAY</p>
    </div>
  </div>
</template>

<script>
import { ipcRenderer } from 'electron'

export default {
  name: 'Drawer-settings',

  computed: {
    isFinished() {
      return this.$store.getters.isFinished
    }
  },

  methods: {
    isFinished() {
      const payload = {
        key: 'isFinished',
        val: !this.isFinished
      }
      ipcRenderer.send('toggle-isFinished', !this.isFinished)
      this.$store.dispatch('setSetting', payload)
      this.$store.dispatch('setViewState', payload)
    }
  }
}
</script>

<style lang="scss" scoped>
.Checkbox {
  background-color: $colorNavy;
  border: 2px solid $colorBlueGrey;
  border-radius: 100%;
  display: inline-block;
  transition: $transitionDefault;
  width: 16px;
  height: 16px;
  &:hover {
    border-color: #FF4384;
  }
  &.is-active {
    background-color: #FF4384;
    border-color: #FF4384;
    &:hover {
      background-color: #FF4384;
      border-color: #FF4384;
    }
  }
}

.Setting-wrapper {
  border-bottom: 1px solid lightblue;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  margin: 12px 0;
  padding: 12px;
}

.Setting-title {
  color: $colorBlueGrey;
  font-size: 14px;
  letter-spacing: 0.05em;
}
</style>
