<template>
  <multiInput v-model="value" />
  <!-- <multiInput /> -->
  <hr />
  {{ value }}
</template>

<script>
import multiInput from "@/components/multiInput.vue";

export default {
  name: "App",
  components: { multiInput },
  data() {
    return {
      value: ["one", "two"],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
