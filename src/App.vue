<template>
  <div id="app">
    <Drums />
  </div>
</template>

<script>
import Drums from "../src/components/Drums.vue";

export default {
  name: "App",
  components: {
    Drums,
  },
};
</script>

<style>
html {
  font-size: 10px;
  background: url("../src/assets/background.jpg") bottom center;
  background-size: cover;
}

body,
html {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}
</style>