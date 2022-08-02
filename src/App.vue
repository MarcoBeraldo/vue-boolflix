<template>
  <div id="app">
    <AppHeader @search="getProductions" />
    <section id="movies">
      <h2>Movies</h2>
      <ProductionCard
        v-for="movie in movies"
        :key="movie.id"
        :production="movie"
      />
    </section>

    <section id="series">
      <h2>Series</h2>
      <ProductionCard
        v-for="serie in series"
        :key="serie.id"
        :production="serie"
      />
    </section>
  </div>
</template>

<script>
import axios from "axios";
import AppHeader from "/src/components/AppHeader.vue";
import ProductionCard from "/src/components/ProductionCard.vue";
export default {
  name: "App",
  components: {
    AppHeader,
    ProductionCard,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        language: "it-IT",
        key: "aedbe765e1515ff23693adb543bba89d",
        baseUri: "https://api.themoviedb.org/3",
      },
    };
  },
  methods: {
    getProductions(query) {
      if (!query) {
        this.movies = this.query = [];
        return;
      }
      const { language, key } = this.api;

      const config = {
        params: {
          api_key: key,
          language,
          query,
        },
      };
      this.fetchData("/search/movie", config, "movies");
      this.fetchData("/search/tv", config, "series");
    },

    fetchData(endpoint, config, target) {
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
        this[target] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
</style>