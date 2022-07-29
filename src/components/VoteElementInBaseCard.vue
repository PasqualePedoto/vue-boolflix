<template>
  <li class="d-flex align-items-center desc">
    <p class="m-0 me-2">Vote:</p>
    <div v-if="changeVoteToStars(vote) === 5">
      <i class="fa-solid fa-star" v-for="star in 5" :key="star + 'a'"></i>
    </div>
    <div v-else-if="changeVoteToStars(vote) === 0">
      <i class="fa-regular fa-star" v-for="star in 5" :key="star + 'b'"></i>
    </div>
    <div v-else>
      <i class="fa-solid fa-star" v-for="star in changeVoteToStars(vote)" :key="star + 'c'"></i>
      <i class="fa-regular fa-star" v-for="star in 5 - changeVoteToStars(vote)" :key="star + 'd'"></i>
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
      return Math.floor(Math.ceil(vote) / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
// Ogni descrizione ha un pò d'aria
.desc {
  padding: 5px 10px;

  p {
    font-weight: bold;
  }
}
</style>
