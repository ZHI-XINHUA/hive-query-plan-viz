<template>
  <div id="graphContainer" ref="con" v-bind:style="`height:${containerSize.height}px`">
    <el-button @click="add">add</el-button>
  </div>
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
      graph: {},
      containerSize: {
        height: 1024
      }
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
  },
  methods: {
    add: function () {
      this.containerSize.height += 100;
      this.graph.changeSize(this.$refs.con.offsetWidth, this.containerSize.height);
      this.graph.fitView();
    }
  }
}
</script>

<style scoped>
#graphContainer {
  border: solid black 1px;
  /*height: 100%;*/
  position: relative;
}

/deep/ .g6-tooltip {
  color: #444;
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 4px;
  box-shadow: rgb(174, 174, 174) 0px 0px 10px;
}
</style>