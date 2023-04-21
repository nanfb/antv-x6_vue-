<template>
  <div>
    <!-- <button @click="add()">内部Add1: {{ num }}</button> -->
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
      <circle class="test" cx="45" cy="45" r="40" stroke="black" stroke-width="2" fill="red" />
      <!-- <rect x="120" y="120" width="70" height="70" stroke="black" fill="green" stroke-width="5" /> -->
    </svg>
  </div>
</template>
  
<script>
export default {
  name: "Count",
  inject: ["getGraph", "getNode"],
  data() {
    return {
      num: 0,
    };
  },
  mounted() {
    const self = this;
    const node = this.getNode();
    // 监听数据改变事件
    node.on("change:data", ({ current }) => {
      self.num = current.num;
    });
  },
  methods: {
    add() {
      const node = this.getNode();
      const { num } = node.getData();
      node.setData({
        num: num + 1,
      });
    },
  },
};
</script>
  