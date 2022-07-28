<template>
  <section id="base-card">
    <ul>
      <li>Original_Title: {{ result.original_title }}</li>
      <li>Title: {{ result.title }}</li>
      <li v-if="result.original_language === 'it' || result.original_language === 'en'">
        <div class="d-flex align-items-center">
          <p>Language:</p>
          <figure class="m-0">
            <img :src="nationFlag(result.original_language)" :alt="nationFlag(result.original_language)" />
          </figure>
        </div>
      </li>
      <li v-else>{{ result.original_language }}</li>
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
  methods: {
    nationFlag(string) {
      return require(`../assets/image/${string}.png`);
    },
  },
};
</script>

<style lang="scss" scoped></style>
