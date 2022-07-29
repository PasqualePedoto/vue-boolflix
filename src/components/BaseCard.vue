<template>
  <section id="base-card">
    <ul id="features-movies-series">
      <!-- Image -->
      <li class="img-height flex-shrink-0">
        <figure class="h-100 m-0">
          <img v-if="result.poster_path !== 'https://image.tmdb.org/t/p/w342null'" :src="result.poster_path" :alt="result.poster_path" />
          <img
            v-else
            src="https://img.pixers.pics/prd_pho(cms:2019/02/5c6ac1e63265e_dr-czarna-40x30-nowycien.png,400,302,s3:400/FO/59/47/47/91/400_FO59474791_a1dfd092f58a037e9ed227119296e100.jpg,367,297,dst_over,11,3,jpg)/poster-in-cornice-grunge-graffiato-striscia-di-pellicola-sporca-bobina-fondo.jpg.jpg"
            alt="not-image"
          />
        </figure>
      </li>
      <li class="h-100">
        <ul class="m-0 p-0" id="info-movies-series">
          <!-- Original Title -->
          <li class="desc mt-2">
            <p class="m-0 me-2 fw-bold">Original_Title:</p>
            <p class="m-0">{{ result.original_title || result.original_name }}</p>
          </li>
          <!-- Title -->
          <li class="desc">
            <p class="m-0 me-2 fw-bold">Title:</p>
            <p class="m-0 me-2">{{ result.title || result.name }}</p>
          </li>
          <!-- Image Language -->
          <li class="flag-language desc" v-if="result.original_language === 'it' || result.original_language === 'en'">
            <div class="d-flex align-items-center">
              <p class="m-0 me-2 fw-bold">Language:</p>
              <figure class="m-0">
                <img class="rounded-2" :src="nationFlag(result.original_language)" :alt="nationFlag(result.original_language)" />
              </figure>
            </div>
          </li>
          <li class="desc" v-else>
            <div class="d-flex align-items-center">
              <p class="m-0 me-2 fw-bold">Language:</p>
              <p class="m-0">{{ result.original_language }}</p>
            </div>
          </li>
          <!-- Vote -->
          <VoteElementInBaseCard :vote="result.vote_average" />
        </ul>
      </li>
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
  data() {
    return {
      notImage: "https://www.scelgonews.it/cinema-cosa-ce-di-nuovo/pellicola-cinema/",
    };
  },
  methods: {
    nationFlag(string) {
      return require(`../assets/image/${string}.png`);
    },
  },
};
</script>

<style lang="scss" scoped>
// ------------------------------------------------------------
// Questo ul fa riferimento a tutta la lista dei films/serie tv
// ------------------------------------------------------------

#features-movies-series {
  // Diamo una width e heigth fissa facendo riferimento alla width di 342px
  // consigliata per la dimensione dell'immagine del film o serie tv
  width: 342px;
  height: 660px;

  // Diamo il display flex in modo tale da mantenere omogenee le dimensioni
  // della foto e della descrizione per ogni film o serie tv
  display: flex;
  flex-direction: column;

  // Tutto centrato
  text-align: center;
  border: 2px solid white;

  // Diamo un pò d'aria col margin e settiamo il padding di BS
  padding: 0;
  margin-top: 10px;

  // Definiamo il colore e il font-size
  color: white;
  font-size: 12px;

  // Fissiamo l'height dell'immagine
  .img-height {
    height: 500px;
  }

  // ------------------------------------------------------------
  // Questi sono i singoli films/serie tv
  // ------------------------------------------------------------

  li {
    display: flex;
    justify-content: center;

    // height: 20px;

    // ------------------------------------------------------------
    // Questa è la lista delle 4 descrizioni del film/serietv
    // ------------------------------------------------------------
    #info-movies-series {
      display: flex;
      flex-direction: column;

      // Col flex-grow-1 facciamo in modo tale che prendi tutto lo spazio
      // disponibile
      flex-grow: 1;

      // Essendo 4 elementi descrittivi dividiamo lo spazio disponibile per 4
      li {
        height: 25%;
        align-items: stretch;
      }
    }
  }

  // Ogni descrizione ha un pò d'aria
  .desc {
    padding: 5px 10px;
  }

  // Settiamo l'altezza della bandiera
  .flag-language {
    height: 50px;

    figure {
      width: 60px;
      height: 30px;
    }
  }
}
</style>
