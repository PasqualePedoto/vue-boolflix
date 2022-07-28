<template>
  <main class="container">
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
  </main>
</template>

<script>
export default {
  name: "BaseMain",
  props: {
    QueryResults: Array,
  },
};
</script>

<style lang="scss" scoped></style>
