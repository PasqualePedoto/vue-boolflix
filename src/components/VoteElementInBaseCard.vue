<template>
  <li class="d-flex align-items-center">
    <p>Vote:</p>
    <div v-if="changeVoteToStars(vote) === 5">
      <i class="fa-solid fa-star" v-for="(star, i) in 5" :key="i"></i>
    </div>
    <div v-else-if="changeVoteToStars(vote) === 0">
      <i class="fa-regular fa-star" v-for="star in 5" :key="star"></i>
    </div>
    <div v-else>
      <i class="fa-solid fa-star" v-for="star in changeVoteToStars(vote)" :key="star"></i>
      <i class="fa-regular fa-star" v-for="star in 5 - changeVoteToStars(vote)" :key="star"></i>
    </div>
  </li>
</template>

<script>
export default {
  name: "VoteElementInBaseCard",
  props: {
    vote: Number,
  },
  methods: {
    changeVoteToStars(vote) {
      let voto = Math.ceil(vote);
      return Math.floor(voto / 2);
    },
  },
};
</script>

<style lang="scss" scoped></style>
