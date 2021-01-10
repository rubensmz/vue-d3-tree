<template>
  <div id="app" class="w-full overflow-hidden">
    <div class="flex">
      <div
        class="bg-indigo-100 rounded-md justify-center items-center flex-initial w-3/12"
      >
        <button
          class="mt-3 focus:outline-none w-32 py-2 rounded-md font-semibold text-white bg-indigo-500 ring-4 ring-indigo-300"
          @click="resetZoom"
        >
          Reset zoom
        </button>
      </div>
      <div class="tree-container flex-1">
        <h1 class="bg-green-500 rounded-md text-white font-bold">Title</h1>
        <tree
          :data="treeData"
          ref="tree"
          v-model="currentData"
          class="tree"
          :nodeTextDisplay="nodeTextDisplay"
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
  methods: {
    resetZoom() {
      if (!this.$refs["tree"]) {
        return;
      }
      this.isLoading = true;
      this.$refs["tree"].resetZoom().then(() => {
        this.isLoading = false;
      });
    },
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
.tree-container {
  width: 100vw;
  height: 100vh;
}
</style>
