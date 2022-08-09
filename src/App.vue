<template>
  <div id="app" class="d-flex flex-column">
    <BaseHeader @search-query="receiveQuery" class="flex-shrink-0" :genres="genres" />
    <BaseMain :query-value="query" :query-movies-results="moviesResults" :query-tvseries-results="tvSeriesResults" class="flex-grow-1 align-items-stretch" />
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
      moviesResults: [],
      tvSeriesResults: [],
      genres: [],

      // Array degli id
      allFilmsId: [],
      allSeriesId: [],
    };
  },
  computed: {
    // Le computed qui definite tengono traccia
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
    // Questa è la funzione che viene invocata al momento del search di
    // un film o di una serie tv
    startSearch() {
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
      this.fetchData(this.searchMovies, config, "moviesResults", "allFilmsId");

      // Chiamata atta a prelevare serie tv
      this.fetchData(this.searchTvSeries, config, "tvSeriesResults", "allSeriesId");
    },

    fetchData(endpoint, config, targetResults, targetId) {
      axios
        .get(`${this.baseUri}${endpoint}`, config)
        .then((res) => {
          // Azzero gli ID delle serie ad ogni chiamata
          this[targetId] = [];

          this[targetResults] = res.data.results.map((element) => {
            // Prelevo l'ID della serie Tv e lo pusho in un array per tenerne traccia
            this[targetId].push(element.id);

            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
          console.log(this[targetResults]);
        })
        .catch((err) => {
          console.err(err);
        });
    },

    // Funzione eseguita al momento dell'arrivo della query
    receiveQuery(query) {
      this.query = query;
      this.startSearch();
    },
    getGenres() {
      const genresConfig = {
        params: {
          api_key: this.api_key,
          language: this.language,
        },
      };
      // Chiamata atta a prelevare i generi
      axios
        .get(this.genresUri, genresConfig)
        .then((res) => {
          this.genres = res.data.genres;
          console.log(this.genres);
        })
        .catch((err) => {
          console.err(err);
        });
    },
  },
  mounted() {
    this.getGenres();
  },
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

#app {
  min-height: 100vh;
}
</style>
