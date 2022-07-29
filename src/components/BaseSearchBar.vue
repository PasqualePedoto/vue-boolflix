<template>
  <nav class="d-flex align-items-center justify-content-center">
    <input type="text" class="form-control me-2" placeholder="Cerca qui" @keyup.enter="emitQuery" @keyup.esc="cancelQuery" v-model.trim="query" />
    <button role="button" class="btn btn-primary" @click="emitQuery">Click!</button>
  </nav>
</template>

<script>
export default {
  name: "BaseSearchBar",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    emitQuery() {
      if (this.query === "") return;
      else this.$emit("search-query", this.query);
    },
    cancelQuery() {
      this.query = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
