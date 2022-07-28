<template>
  <section id="movies-section">
    <ul>
      <li v-for="(result, index) in QueryResults" :key="index">
        <BaseCard :result="result" />
      </li>
    </ul>
  </section>
</template>

<script>
import BaseCard from "./BaseCard.vue";
export default {
  name: "MoviesSection",
  props: {
    QueryResults: Array,
  },
  components: { BaseCard },
};
</script>

<style lang="scss" scoped></style>
