<template>
  <div>
    <div>
      <img alt="Vue logo" src="./assets/logo.png" />
      <HelloWorld msg="Hello Vue 3.0 + Vite" />
    </div>
    <div>
      <PlayGround />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import PlayGround from "./components/PlayGround.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    PlayGround,
  },
};
</script>