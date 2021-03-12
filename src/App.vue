<template>
  <div id="app">
    <HelloWorld />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import vuescroll from "vuescroll";

@Component({
  components: {
    HelloWorld,
    vuescroll
  }
})
export default class App extends Vue {}
</script>

<style>
#app {
  height: 100%;
  width: 100%;
}
</style>
