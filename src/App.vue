<template>
  <div id="app" class="w-full overflow-hidden">
    <div class="flex">
      <div
        class="bg-indigo-100 rounded-md justify-center items-center flex-initial w-3/12"
      >
        <p class="content-center mt-4">
          <span>Layout: </span>
          <select name="layout" id="layout" v-model="layout">
            <option value="horizontal">Horizontal</option>
            <option value="vertical">Vertical</option>
            <option value="circular">Circular</option>
          </select>
        </p>
        <p class="content-center mt-2">
          <span>X distance: </span>
          <input
            type="range"
            :min="-maxMargin"
            :max="0"
            v-model.number="marginX"
            class="reversed-direction"
          />
        </p>
        <p class="content-center mt-2">
          <span>Y distance: </span>
          <input
            type="range"
            :min="-maxMargin"
            :max="0"
            v-model.number="marginY"
            class="reversed-direction"
          />
        </p>
        <p class="mt-2">
          <button
            class="mt-3 focus:outline-none w-64 py-2 rounded-md font-semibold text-white bg-indigo-500 ring-4 ring-indigo-300"
            @click="resetZoom"
          >
            Reset zoom
          </button>
        </p>
        <p class="mt-2">
          <button
            class="mt-3 focus:outline-none w-64 py-2 rounded-md font-semibold text-white bg-green-500 ring-4 ring-green-300"
            @click="downloadImage"
          >
            Download image
          </button>
        </p>
      </div>
      <div class="tree-container flex-1">
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
          :margin-x="marginX"
          :margin-y="marginY"
          :radius="radius"
          :layoutType="layout"
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
import d3ToPng from "d3-svg-to-png";

export default {
  name: "App",
  components: { tree },
  data: function() {
    return {
      treeData: json_data,
      type: "tree",
      layout: "horizontal",
      duration: 750,
      maxMargin: 200,
      marginX: 0,
      marginY: 0,
      radius: 3,
      leafTextMargin: 6,
      nodeTextMargin: 6,
      nodeText: "name",
      currentData: null,
      zoomable: true,
      isLoading: false,
      nodeTextDisplay: "all",
      linkLayout: "bezier",
      minZoom: 0.1,
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
    downloadImage() {
      d3ToPng("svg", "name.png", {
        scale: 3,
        format: "png",
        quality: 1,
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
.reversed-direction {
  direction: rtl;
}
</style>
