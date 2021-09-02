<template>
  <div>
    <h1>{{ gameTitle }}</h1>
    <h2>{{ madeWith }}</h2>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    gameTitle: String,
    madeWith: String,
  },
};
</script>
