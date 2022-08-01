<template>
  <div id="app" @clicked-search="getMovies">
    <AppHeader />
  </div>
</template>

<script>
import axios from "axios";
import AppHeader from "/src/components/AppHeader.vue";
export default {
  name: "App",
  components: {
    AppHeader,
  },
  data() {
    return {
      query: "",
      movies: [],
      series: [],
    };
  },
  methods: {
    getMovies() {
      this.fetchMovie();
      this.fetchSerie();
    },
    fetchMovie() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=aedbe765e1515ff23693adb543bba89d&query=${this.query}&language=it-IT`
        )
        .then((res) => {
          this.movies = res.data.results;
        });
    },
    fetchSerie() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=aedbe765e1515ff23693adb543bba89d&query=${this.query}&language=it-IT`
        )
        .then((res) => {
          this.series = res.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
</style>
