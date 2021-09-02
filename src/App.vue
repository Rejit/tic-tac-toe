<template>
  <div>
    <div class="container1">
      <img alt="Vue logo" src="./assets/logo.png" />
      <HelloWorld :gameTitle="gameTitle" :madeWith="madeWith" />
    </div>
    <div class="container2">
      <PlayGround />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import PlayGround from "./components/PlayGround.vue";

export default {
  name: "App",
  data() {
    return {
      gameTitle: "Tic-Tac-Toe",
      madeWith: "Hello Vue 3.0 + Vite",
    };
  },
  components: {
    HelloWorld,
    PlayGround,
  },
};
</script>
<style scoped>
.container1 {
  margin: auto;
  width: 30%;
  display: inline-block;
}
.container2 {
  margin: auto;
  width: 70%;
  display: inline-block;
}
</style>