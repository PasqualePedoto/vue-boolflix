<template>
  <section id="results-section">
    <div class="text-white h2" v-if="queryResults.length != 0">{{ titolo }}</div>
    <div v-else class="h2 text-white">Non sono stati prodotti risultati per {{ titolo }}</div>
    <ul>
      <li v-for="(result, index) in queryResults" :key="index">
        <BaseCard :result="result" />
      </li>
    </ul>
  </section>
</template>

<script>
import BaseCard from "./BaseCard.vue";
export default {
  name: "ResultsSection",
  props: {
    queryResults: Array,
    titolo: String,
  },
  components: { BaseCard },
};
</script>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-wrap: wrap;

  li {
    width: calc(100% / 3 - 10px);
  }
}
</style>
