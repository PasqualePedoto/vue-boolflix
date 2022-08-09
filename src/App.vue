<template>
  <div id="app" class="d-flex flex-column">
    <BaseHeader @search-query="receiveQuery" class="flex-shrink-0" :genres="genres" />
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
          // Azzero l'array degli ID dei films ad ogni chiamata
          this.allFilmsId = [];

          this.movieResults = res.data.results.map((element) => {
            // Prelevo l'ID del film e lo pusho in un array per tenerne traccia
            this.allFilmsId.push(element.id);

            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
          console.log("Films: " + this.allFilmsId.length);
        })
        .catch((err) => {
          console.err(err);
        });

      // Chiamata atta a prelevare serie tv
      axios
        .get(this.tvSeriesUri, config)
        .then((res) => {
          // Azzero gli ID delle serie TV ad ogni chiamata
          this.allSeriesId = [];

          this.tvSeriesResults = res.data.results.map((element) => {
            // Prelevo l'ID della serie Tv e lo pusho in un array per tenerne traccia
            this.allSeriesId.push(element.id);

            const imageLink = this.initialImageLink + this.imageDimensione + element["poster_path"];
            element["poster_path"] = imageLink;
            return element;
          });
          console.log("Series: " + this.allSeriesId.length);
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
