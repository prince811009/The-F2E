<template>
  <div class="Dial-wrapper">
    <div class="newMission">
      <input class="inputText" type="text" v-model="addText" placeholder="ADD A NEW MISSION..."/>
    </div>
  </div>
</template>

<script>

export default {
}
</script>

<style lang="scss" scoped>
.inputText {
  display: flex;
  width: 445px;
  height : 56px;
  position: absolute;
  top: 48px;
  left: 85px;
  border-style: none;
  font-family: 'Roboto';
  color: #FF4384;
  box-sizing: border-box;
  padding: 19px 226px 18px 16px;
}

</style>
