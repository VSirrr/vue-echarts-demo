<template>
  <div id="app">
    <Demo1 />
    <SDMap />
  </div>
</template>

<script>
import Demo1 from "./components/Demo1.vue";
import SDMap from "./components/SDMap.vue";

export default {
  name: "App",
  components: {
    Demo1,
    SDMap,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
