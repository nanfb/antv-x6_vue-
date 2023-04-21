<template>
  <div class="gras">
    <div id="canvas"></div>
    <button @click="add">外部 Add</button>
  </div>
</template>

<script>
import { Graph } from "@antv/x6";
import "@antv/x6-vue-shape";
import Count from "./modes/node.vue";

let graph = null;
export default {
  name: "App",
  mounted() {
    graph = new Graph({
      container: document.getElementById("canvas"),
      width: 600,
      height: 400,
      // 自动吸附
      connecting: {
        snap: true,
      },
      //节点大小可修改
      resizing: {
        enabled: true,
      },
      grid: {
        visible: true,
        size: 5,
      },
    });

    // 方式1：注册 vue component
    Graph.registerVueComponent(
      "count",
      {
        template: `<Count />`,
        components: {
          Count,
        },
      },
      true
    );

    // 方式2：注册 vue component
    Graph.registerNode("my-count", {
      inherit: "vue-shape",
      x: 200,
      y: 150,
      width: 150,
      height: 100,
      component: {
        template: `<Count />`,
        components: {
          Count,
        },
      },
    });

    graph.addNode({
      id: "1",
      shape: "vue-shape",
      x: 200,
      y: 150,
      width: 150,
      height: 100,
      component: "count",
      data: {
        num: 0,
      },
    });
    graph.addNode({
      id: "2",
      shape: "my-count",
      x: 400,
      y: 150,
      width: 150,
      height: 100,
      data: {
        num: 0,
      },
    });
  },
  methods: {
    add() {
      const nodes = graph.getNodes();
      if (nodes.length) {
        nodes.forEach((node) => {
          const { num } = node.getData();
          node.setData({
            num: num + 1,
          });
        });
      }
    },
  },
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.gras {
  border: 1px solid #ccc;
  width: 600px;
  height: 400px;
  display: flex;
}
</style>
