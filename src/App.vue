<template>
  <div id="app">
    <Step msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import Step from "./components/Step.vue";

export default {
  name: "App",
  components: {
    Step,
  },
};
</script>