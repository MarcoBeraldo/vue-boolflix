<template>
  <header>
    <input v-model="query" />
    <button @click="getMovies">Cerca</button>
  </header>
</template>

<script>
import axios from "axios";
export default {
  name: "AppHeader",
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

<style>
</style>