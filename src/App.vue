<template>
  <div id="app" class="d-flex flex-column">
    <BaseHeader @search-query="receiveQuery" class="flex-shrink-0" />
    <BaseMain :query-value="query" :query-movies-results="movieResults" :query-tvseries-results="tvSeriesResults" class="flex-grow-1 align-items-stretch" />
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
      searchGenres: "/genre/movie/list",

      // Parametri da passare alla query
      language: "it-IT",
      query: "",
      api_key: "94e919df475d5245ad0600c98048db21",

      // Start link della foto e dimension
      initialImageLink: "https://image.tmdb.org/t/p/",
      imageDimensione: "w342",

      // Array che manterranno i risultati della query sia delle serieTV
      // che per quanto riguarda i films e i generi
      movieResults: [],
      tvSeriesResults: [],
      genres: [],
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
    genresUri() {
      return this.baseUri + this.searchGenres;
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
          this.movieResults = res.data.results.map((element) => {
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
          this.tvSeriesResults = res.data.results.map((element) => {
            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
        })
        .catch((err) => {
          console.err(err);
        });
    },

    // Funzione eseguita al momento dell'arrivo della query
    receiveQuery(query) {
      this.query = query;
      this.getMoviesFromTheMovieDB();
    },
  },
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

#app {
  min-height: 100vh;
}
</style>
