<template>
  <div id="app">
    <div class="container">
      <tree
        :data="treeData"
        ref="tree"
        v-model="currentData"
        class="tree"
        :nodeTextDisplay="nodeTextDisplay"
        :identifier="getId"
        :nodeTextMargin="nodeTextMargin"
        :zoomable="zoomable"
        :leafTextMargin="leafTextMargin"
        :node-text="nodeText"
        :margin-x="Marginx"
        :margin-y="Marginy"
        :radius="radius"
        :layoutType="layoutType"
        :duration="duration"
        :minZoom="minZoom"
        :maxZoom="maxZoom"
      ></tree>
    </div>
  </div>
</template>

<script>
import { tree } from "vued3tree";
import json_data from "@/assets/data/tree.json";

export default {
  name: "App",
  components: { tree },
  data: function() {
    return {
      treeData: json_data,
      type: "tree",
      layoutType: "horizontal",
      duration: 750,
      Marginx: 30,
      Marginy: 30,
      radius: 3,
      leafTextMargin: 6,
      nodeTextMargin: 6,
      nodeText: "name",
      currentData: null,
      zoomable: true,
      isLoading: false,
      nodeTextDisplay: "all",
      linkLayout: "bezier",
      minZoom: 0.8,
      maxZoom: 9,
      events: [],
    };
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
}
.tree {
  width: 100%;
  height: 100%;
}
.container {
  width: 100vw;
  height: 100vh;
}
</style>
