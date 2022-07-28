<template>
  <main class="container">
    <MoviesSection :query-results="QueryResults" />
  </main>
</template>

<script>
import MoviesSection from "./MoviesSection.vue";
export default {
  name: "BaseMain",
  components: {
    MoviesSection,
  },
  props: {
    QueryResults: Array,
  },
};
</script>

<style lang="scss" scoped></style>
