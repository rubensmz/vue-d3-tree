<template>
  <div id="app">
    <div class="container">
      <tree :data="treeData" node-text="name" layoutType="horizontal" class="tree"></tree>
    </div>
  </div>
</template>

<script>
import { tree } from "vued3tree";
import json_data from "@/assets/tree.json";

export default {
  name: "App",
  components: { tree },
  data: function() {
    return {
      treeData: json_data,
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
.container{
    width: 100vw;
    height: 100vh;
}
</style>
