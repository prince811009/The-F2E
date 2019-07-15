<template>
  <div class="Container">
    <p class="Drawer-heading">TO-DO</p>
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
      <p class="Setting-title">THE FOURTH THING TO DO TODAY</p>
    </div>
    <p class="Drawer-footer">DONE</p>
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
.Container {
  width: 445px;
  position: absolute;
  top: 200px;
  left: 630px;
}

.Drawer-heading {
  background: #727d98;
  box-sizing: border-box;
  width: 445px;
  height: 44px;
  padding: 8px 340px 8px 16px;
  line-height: 24px;
  font-size: 24px;
  letter-spacing: 0.05em;
}

.Drawer-footer {
  background: #727d98;
  box-sizing: border-box;
  position: absolute;
  margin-top: 45px;
  width: 445px;
  height: 44px;
  padding: 8px 330px 8px 16px;
  line-height: 24px;
  font-size: 24px;
  letter-spacing: 0.05em;
}

.Checkbox {
  box-sizing: border-box;
  border: 2px solid white;
  border-radius: 100%;
  display: inline-block;
  transition: $transitionDefault;
  width: 24px;
  height: 24px;
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
  justify-content: flex-start;
  margin: 12px 5px;
  padding: 15px;
}

.Setting-title {
  display: flex;
  text-align: center;
  line-height: 24px;
  color: white;
  font-size: 14px;
  letter-spacing: 0.05em;
  margin-left: 30px;
}
</style>
