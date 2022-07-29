<template>
  <header>
    <div class="container">
      <div class="row">
        <div class="col">
          <div class="d-flex align-items-center justify-content-between">
            <a href="#"><h1>Boolfix</h1></a>
            <BaseSearchBar @search-query="emitQuery" />
          </div>
        </div>
      </div>
    </div>
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

<style lang="scss" scoped>
header {
  background-color: #000;

  a {
    color: red;
    margin: 10px;

    h1 {
      font-weight: bold;
      margin: 0;
    }
  }
}
</style>
