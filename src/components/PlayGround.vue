<template>
  <div class="container">
    <div class="control-panel">{{ winner }}</div>
    <div class="control-panel">{{ grid }}</div>
    <div class="game-panel">
      <div v-for="(row, i) in grid" :key="i" class="row">
        <div
          v-for="(col, j) in row"
          :key="j"
          :class="getClass(i, j)"
          @click="setToken(i, j)"
          @dblclick="setToken(i, j, -1)"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
export default {
  name: "PlayGround",
  setup() {
    const grid = ref([
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ]);
    const getClass = (row, col, solvedClass = "path ") => {
      if (row === 0 || row === 1) solvedClass += "bl ";
      if (row === 1 || row === 2) solvedClass += "tl ";
      if (col === 0 || col === 1) solvedClass += "rl ";
      if (col === 1 || col === 2) solvedClass += "ll ";
      if (grid.value[row][col] === 1) solvedClass += "usr";
      else if (grid.value[row][col] === -1) solvedClass += "cpu";

      return solvedClass;
    };
    const setToken = (row, col, value = 1) => {
      if (grid.value[row][col] === null) {
        grid.value[row][col] = value;
      }
    };
    const operateLine = (val) =>
      // Win by row
      grid.value[0][0] + grid.value[0][1] + grid.value[0][2] === val ||
      grid.value[1][0] + grid.value[1][1] + grid.value[1][2] === val ||
      grid.value[2][0] + grid.value[2][1] + grid.value[2][2] === val ||
      // Win by col
      grid.value[0][0] + grid.value[1][0] + grid.value[2][0] === val ||
      grid.value[0][1] + grid.value[1][1] + grid.value[2][1] === val ||
      grid.value[0][2] + grid.value[1][2] + grid.value[2][2] === val ||
      // Win by diagonal
      grid.value[0][0] + grid.value[1][1] + grid.value[2][2] === val ||
      grid.value[2][0] + grid.value[1][1] + grid.value[0][2] === val;
    const winner = computed(() => {
      return operateLine(3) ? "USER" : operateLine(-3) ? "CPU" : false;
    });
    return {
      grid,
      getClass,
      setToken,
      winner,
    };
  },
};
</script>
<style scoped>
.control-panel {
  width: 90%;
  margin: auto;
  background-color: cadetblue;
}
.game-panel {
  margin: auto;
  width: 90%;
  background-color: green;
}
.path {
  background-color: grey;
  width: 33%;
  height: 100%;
  display: inline-block;
}
.path:hover {
  background-color: tomato;
  cursor: pointer;
}
.row {
  width: 100%;
  height: 70px;
}
.container {
  margin: auto;
  width: 40%;
  padding: 10px;
}
.bl {
  border-bottom: 1px solid black;
}
.tl {
  border-top: 1px solid black;
}
.rl {
  border-right: 1px solid black;
}
.ll {
  border-left: 1px solid black;
}
.usr {
  background-color: red;
}
.cpu {
  background-color: blue;
}
</style>