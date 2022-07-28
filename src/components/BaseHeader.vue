<template>
  <header class="container d-flex align-items-center justify-content-between">
    <h1>Boolfix</h1>
    <BaseSearchBar />
  </header>
</template>

<script>
import BaseSearchBar from "./BaseSearchBar.vue";
export default {
  name: "BaseHeader",
  components: { BaseSearchBar },
};
</script>

<style lang="scss" scoped></style>
