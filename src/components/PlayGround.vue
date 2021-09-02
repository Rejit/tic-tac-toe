<template>
  <div class="container">
    <div class="control-panel">
      <div v-if="winner">{{ winner }}</div>
    </div>
    <div class="game-panel">
      <div class="tic-tac-toe">
        <div class="separator vertical left"></div>
        <div class="separator vertical right"></div>
        <div class="separator horizontal top"></div>
        <div class="separator horizontal bottom"></div>
        <div v-for="(row, i) in grid" :key="i">
          <div
            v-for="(col, j) in row"
            :key="j"
            class="path"
            @click="setToken(i, j)"
            @dblclick="setToken(i, j, -1)"
          >
            <img v-if="grid[i][j] === 1" alt="o" src="./../assets/o.png" />
            <img v-if="grid[i][j] === -1" alt="x" src="./../assets/x.png" />
          </div>
        </div>
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
    const setToken = (row, col, value = 1) => {
      grid.value[row][col] = value;
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
      setToken,
      winner,
    };
  },
};
</script>
<style scoped>
.container {
  margin: auto;
  width: 100%;
  padding: 10px;
}
.control-panel {
  width: 40%;
  display: inline-block;
  margin: auto;
  background-color: cadetblue;
}
.game-panel {
  width: 40%;
  display: inline-block;
  margin: auto;
}
.tic-tac-toe {
  position: relative;
  width: 300px;
  height: 300px;
  margin: auto;
}
.separator {
  background-color: rgb(209 20 20);
  position: absolute;
  border-radius: 0px 5px 0px 5px;
}
.vertical {
  width: 1%;
  height: 100%;
}
.horizontal {
  height: 1%;
  width: 100%;
}
.left {
  margin-left: 33%;
}
.right {
  margin-left: 66%;
}
.top {
  margin-top: 33%;
}
.bottom {
  margin-top: 66%;
}
.path {
  width: 33%;
  height: 98px;
  display: inline-block;
}
.path:hover {
  cursor: pointer;
}
img {
  top: 0;
  width: 90%;
  height: inherit;
}
</style>