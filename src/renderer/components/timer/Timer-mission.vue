<template>
  <div class="todolist">
   <div class="newMission">
      <input class="inputText" type="text" v-model="addText" placeholder="ADD A NEW MISSION..."/>
      <img src="../../assets/add.png"/>
    </div>
    <div class="list">
      <ul>
        <li v-for="(item, index) in list" :key="index">
          <div class="todolistall">
            <span class="todolistmain">{{item.main}}</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      list: [
        { main: 'THE FIRST THING TO DO TODAY', id: 1 },
        { main: 'THE SECOND THING TO DO TODAY', id: 2 },
        { main: 'THE THIRD THING TO DO TODAY', id: 3 }
      ]
    }
  }
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

.list {
  width: 445px;
  height: 32px;
  position: absolute;
  top: 613px;
  left: 100px;
  font-family: "Roboto";
  font-size: 16px;
  font-weight: bold;
  color: #003164;
  padding: 3px 182px 10px 2px;
  list-style-type: circle;
}

</style>
