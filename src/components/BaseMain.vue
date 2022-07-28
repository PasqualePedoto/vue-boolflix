<template>
  <main class="container">
    <ResultsSection titolo="Movies" :query-results="QueryMoviesResults" />
    <ResultsSection titolo="Serie Tv" :query-results="QueryTvseriesResults" />
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
    QueryMoviesResults: Array,
    QueryTvseriesResults: Array,
  },
};
</script>

<style lang="scss" scoped></style>
