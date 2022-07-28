<template>
  <section id="base-card">
    <ul>
      <!-- Image -->
      <li>
        <figure>
          <img :src="result.poster_path" :alt="result.poster_path" />
        </figure>
      </li>
      <!-- Original Title -->
      <li>Original_Title: {{ result.original_title || result.original_name }}</li>
      <!-- Title -->
      <li>Title: {{ result.title || result.name }}</li>
      <!-- Image Language -->
      <li v-if="result.original_language === 'it' || result.original_language === 'en'">
        <div class="d-flex align-items-center">
          <p>Language:</p>
          <figure class="m-0">
            <img :src="nationFlag(result.original_language)" :alt="nationFlag(result.original_language)" />
          </figure>
        </div>
      </li>
      <li v-else>{{ result.original_language }}</li>
      <!-- Vote -->
      <VoteElementInBaseCard :vote="result.vote_average" />
    </ul>
  </section>
</template>

<script>
import VoteElementInBaseCard from "./VoteElementInBaseCard.vue";
export default {
  name: "BaseCard",
  components: { VoteElementInBaseCard },
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
