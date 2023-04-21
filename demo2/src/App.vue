<template>
  <div id="app">
    <div class="vueNode">
          <HelloWorld/>
    </div>

    <test></test>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import test from './components/test.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,test
  },
}
</script>

<style >

</style>
