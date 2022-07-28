<template>
  <div>
    <BaseHeader @search-query="receiveQuery" />
    <BaseMain :query-movies-results="MovieResults" :query-tvseries-results="TvSeriesResults" />
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
      searchTvSeries: "/search/tv",

      // Parametri da passare alla query
      language: "it-IT",
      query: "",
      api_key: "94e919df475d5245ad0600c98048db21",

      // Start link della foto e dimension
      initialImageLink: "https://image.tmdb.org/t/p/",
      imageDimensione: "w342",

      // Array che manterranno i risultati della query sia delle serieTV
      // che per quanto riguarda i films
      MovieResults: [],
      TvSeriesResults: [],
    };
  },
  computed: {
    // La computed qui definita tiene traccia
    // delle Uri modificate in funzione di cosa cerchiamo
    moviesUri() {
      return this.baseUri + this.searchMovies;
    },
    tvSeriesUri() {
      return this.baseUri + this.searchTvSeries;
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
      // Chiamata atta a prelevare i films
      axios
        .get(this.moviesUri, config)
        .then((res) => {
          this.TvSeriesResults = res.data.results.map((element) => {
            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
        })
        .catch((err) => {
          console.err(err);
        });

      // Chiamata atta a prelevare serie tv
      axios
        .get(this.tvSeriesUri, config)
        .then((res) => {
          this.TvSeriesResults = res.data.results.map((element) => {
            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
        })
        .catch((err) => {
          console.err(err);
        });
    },
    receiveQuery(query) {
      this.query = query;
      this.getMoviesFromTheMovieDB();
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
