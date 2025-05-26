<template>
  <div id="app">
    <TextTransformer />
  </div>
</template>

<script>
import TextTransformer from "./components/TextTransformer.vue";

export default {
  name: "App",
  components: {
    TextTransformer,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 20px;
}
</style>


