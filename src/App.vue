<template>
  <div id="app">
    <app-background></app-background>
  </div>
</template>

<script>
import Background from "./components/Background.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    appBackground: Background
  },
  beforeCreate() {},
  created() {},
  mounted() {}
};
</script>

<style>
body {
  height: 100vh;
}

#app {
  height: 100vh;
}
</style>
