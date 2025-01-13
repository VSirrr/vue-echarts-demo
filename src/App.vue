<template>
  <div id="app">
    <Demo1 />
    <SDMap />
    <AreaChart />
  </div>
</template>

<script>
import Demo1 from "./components/Demo1.vue";
import SDMap from "./components/SDMap.vue";
import AreaChart from "./components/AreaChart.vue";

export default {
  name: "App",
  components: {
    Demo1,
    SDMap,
    AreaChart,
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
