<template>
  <div id="graphContainer" ref="con"></div>
</template>

<script>
import eventBus from "../eventBus/event-bus";
import getGraphData from "../api/query-plan-handler"
import graphRender from "../api/graph-render"
import initG6Graph from "../api/init-g6-graph";

export default {
  name: "PlanGraph",
  data: function () {
    return {
      graphData: {},
      graph: {}
    }
  },
  created() {
    eventBus.$on('textChange', (text) => {
      this.graphData = getGraphData(text);
      graphRender(this.graph, this.graphData);
    })
  },
  mounted() {
    this.graph = initG6Graph(this.$refs.con);
  }
}
</script>

<style scoped>
#graphContainer {
  border: solid black 1px;
  height: 2048px;
}
</style>