<template>
  <main>
    <div class="container h-100">
      <div class="row h-100">
        <div class="col">
          <div v-if="QueryValue !== ''" class="h-100">
            <ResultsSection titolo="Movies" :query-results="QueryMoviesResults" />
            <ResultsSection titolo="Serie Tv" :query-results="QueryTvseriesResults" />
          </div>
          <div v-else class="m-5 text-center h-100 text-white h-100">
            <h2>Cerca film o serie tv</h2>
          </div>
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
    QueryValue: String,
  },
};
</script>

<style lang="scss" scoped>
main {
  background-color: #434343;
  height: 100%;
}
</style>
