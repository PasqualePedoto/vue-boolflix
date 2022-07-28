<template>
  <main class="container">
    <ResultsSection :query-results="QueryResults" />
  </main>
</template>

<script>
import ResultsSection from "./ResultsSection.vue";
export default {
  name: "BaseMain",
  components: {
    ResultsSection,
  },
  props: {
    QueryResults: Array,
  },
};
</script>

<style lang="scss" scoped></style>
