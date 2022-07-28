<template>
  <header class="container d-flex align-items-center justify-content-between">
    <h1>Boolfix</h1>
    <BaseSearchBar @search-query="emitQuery" />
  </header>
</template>

<script>
import BaseSearchBar from "./BaseSearchBar.vue";
export default {
  name: "BaseHeader",
  components: { BaseSearchBar },
  methods: {
    emitQuery(query) {
      this.$emit("search-query", query);
    },
  },
};
</script>

<style lang="scss" scoped></style>
