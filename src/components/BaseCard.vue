<template>
  <section id="base-card">
    <ul>
      <li>Original_Title: {{ result.original_title }}</li>
      <li>Title: {{ result.title }}</li>
      <li>Language: {{ result.original_language }}</li>
      <li>Title: {{ result.vote_average }}</li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "BaseCard",
  props: {
    result: Object,
  },
};
</script>

<style lang="scss" scoped></style>
