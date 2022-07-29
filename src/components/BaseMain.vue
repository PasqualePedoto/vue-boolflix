<template>
  <main>
    <div class="container">
      <div class="row">
        <div class="col">
          <ResultsSection titolo="Movies" :query-results="QueryMoviesResults" />
          <ResultsSection titolo="Serie Tv" :query-results="QueryTvseriesResults" />
        </div>
      </div>
    </div>
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

<style lang="scss" scoped>
main {
  background-color: #434343;
  height: 100%;
}
</style>
