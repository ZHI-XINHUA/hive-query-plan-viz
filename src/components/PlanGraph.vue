<template>
  <div ref="parent">
    <div class="block">
      <span class="demonstration">高度</span>
      <el-slider v-model="containerSize.height" :max="4096" :min="0"></el-slider>
      <span class="demonstration">宽度</span>
      <el-slider v-model="containerSize.width" :max="2048" :min="0"></el-slider>
    </div>
    <div id="graphContainer" ref="con"
         v-bind:style="containerStyle"></div>
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
        height: 0,
        width: 0,
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
    this.containerSize.width = this.$refs.parent.offsetWidth;
    this.containerSize.height = this.$refs.parent.offsetHeight;
    console.log(this.$refs.parent)
  },
  methods: {
    add: function () {
      this.containerSize.height += 100;
      this.graph.changeSize(this.containerSize, this.containerSize.height);
      this.graph.fitView();
    }
  },
  computed: {
    containerStyle: function () {
      this.graph.changeSize(this.containerSize, this.containerSize.height);
      this.graph.fitView();
      return {height: `${this.containerSize.height}px`, width: `${this.containerSize.width}px`};
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