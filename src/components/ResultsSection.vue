<template>
  <section id="results-section">
    <h2 class="text-white" v-if="queryResults.length != 0">{{ titolo }}</h2>
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
