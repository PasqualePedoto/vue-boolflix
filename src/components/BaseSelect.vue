<template>
  <select name="genres" id="">
    <option :value="genre.name" v-for="genre in genres" :key="genre.id">{{ genre.name }}</option>
  </select>
</template>

<script>
export default {
  name: "BaseSelect",
  props: {
    genres: Array,
  },
};
</script>

<style scoped lang="scss"></style>
