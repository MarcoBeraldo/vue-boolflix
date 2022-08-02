<template>
  <div id="app">
    <AppHeader @search="getMovies" />
    <section id="movies">
      <ul v-for="movie in movies" :key="movie.id">
        <li>{{ movie.title }}</li>
        <li>{{ movie.original_title }}</li>
        <li>{{ movie.original_language }}</li>
        <li>{{ movie.vote_average }}</li>
      </ul>
    </section>
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
      movies: [],
      series: [],
    };
  },
  methods: {
    getMovies(query) {
      this.fetchMovie(query);
      this.fetchSerie(query);
    },

    fetchMovie(query) {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=aedbe765e1515ff23693adb543bba89d&query=${query}&language=it-IT`
        )
        .then((res) => {
          this.movies = res.data.results;
        });
    },

    fetchSerie(query) {
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=aedbe765e1515ff23693adb543bba89d&query=${query}&language=it-IT`
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
