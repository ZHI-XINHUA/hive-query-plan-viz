<template>
  <div id="app">
    <QueryPlanViz></QueryPlanViz>
  </div>
</template>

<script>
import QueryPlanViz from "./components/QueryPlanViz";

export default {
  name: 'app',
  components: {
    QueryPlanViz
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
