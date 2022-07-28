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
      <li class="d-flex align-items-center">
        <p>Vote:</p>
        <div v-if="changeVoteToStars(result.vote_average) === 5">
          <i class="fa-solid fa-star" v-for="(star, i) in 5" :key="i"></i>
        </div>
        <div v-else-if="changeVoteToStars(result.vote_average) === 0">
          <i class="fa-regular fa-star" v-for="star in 5" :key="star"></i>
        </div>
        <div v-else>
          <i class="fa-solid fa-star" v-for="star in changeVoteToStars(result.vote_average)" :key="star"></i>
          <i class="fa-regular fa-star" v-for="star in 5 - changeVoteToStars(result.vote_average)" :key="star"></i>
        </div>
      </li>
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
    changeVoteToStars(vote) {
      let voto = Math.ceil(vote);
      return Math.floor(voto / 2);
    },
  },
};
</script>

<style lang="scss" scoped></style>
