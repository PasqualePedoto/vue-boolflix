<template>
  <header class="container d-flex align-items-center justify-content-between">
    <h1>Boolfix</h1>
    <div class="d-flex align-items-center justify-content-center">
      <input type="text" class="form-control me-2" placeholder="Cerca qui" @keyup.enter="emitQuery" @keyup.esc="cancelQuery" v-model="query" />
      <button role="button" class="btn btn-primary" @click="emitQuery">Click!</button>
    </div>
  </header>
</template>

<script>
export default {
  name: "BaseHeader",
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
