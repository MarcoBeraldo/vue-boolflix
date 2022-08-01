<template>
  <header>
    <input v-model="query" />
    <button @click="getMovies">Cerca</button>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    getMovies() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=aedbe765e1515ff23693adb543bba89d&query=${query}&language=it-IT`
        )
        .then((res) => {
          this.movies = res.data.results;
        });
    },
  },
};
</script>

<style>
</style>