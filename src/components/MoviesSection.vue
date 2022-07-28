<template>
  <section id="movies-section">
    <ul>
      <li v-for="(result, index) in QueryResults" :key="index">
        <ul>
          <li>Original_Title: {{ result.original_title }}</li>
          <li>Title: {{ result.title }}</li>
          <li>Language: {{ result.original_language }}</li>
          <li>Title: {{ result.vote_average }}</li>
        </ul>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "MoviesSection",
  props: {
    QueryResults: Array,
  },
};
</script>

<style lang="scss" scoped></style>
