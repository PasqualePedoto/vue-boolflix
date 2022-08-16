<template>
  <header>
    <div class="container">
      <div class="row">
        <div class="col">
          <div class="m-2 d-flex align-items-center justify-content-between">
            <a href="#"><h1 class="m-0">Boolfix</h1></a>
            <div class="d-flex align-items-center justify-content-center">
              <BaseSearchBar @search-query="emitQuery" />
            </div>
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

    h1 {
      font-weight: bold;
      margin: 0;
    }
  }
}
</style>
