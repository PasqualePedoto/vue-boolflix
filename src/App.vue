<template>
  <div>
    <BaseHeader />
  </div>
</template>

<script>
import BaseHeader from "./components/BaseHeader.vue";
// import axios from "axios";

export default {
  name: "App",
  components: {
    BaseHeader,
  },
  data() {
    return {
      TheMovieResults: [],
    };
  },
  methods: {},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
