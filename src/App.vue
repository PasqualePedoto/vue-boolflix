<template>
  <div>
    <BaseHeader />
    <BaseMain :query-results="theMovieResults" />
  </div>
</template>

<script>
import BaseHeader from "./components/BaseHeader.vue";
import BaseMain from "./components/BaseMain.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    BaseHeader,
    BaseMain,
  },
  data() {
    return {
      // Definiamo l'Uri base e le specifiche
      baseUri: "https://api.themoviedb.org/3",
      searchMovies: "/search/movie",

      // Parametri da passare alla query
      language: "it-IT",
      query: "anelli",
      api_key: "94e919df475d5245ad0600c98048db21",

      //Array che manterrà i risultati della query
      theMovieResults: [],
    };
  },
  computed: {
    // La computed qui definita tiene traccia
    // delle Uri modificate in funzione di cosa cerchiamo
    moviesUri() {
      return this.baseUri + this.searchMovies;
    },
  },
  methods: {
    getMoviesFromTheMovieDB() {
      // Definiamo un set di parametri da passare alla
      // chiamata verso l'API
      const config = {
        params: {
          api_key: this.api_key,
          query: this.query,
          language: this.language,
        },
      };

      axios
        .get(this.moviesUri, config)
        .then((res) => {
          this.theMovieResults = res.data.results;
        })
        .catch((err) => {
          console.err(err);
        });
    },
  },
  mounted() {
    this.getMoviesFromTheMovieDB();
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
