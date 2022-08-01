<template>
  <header>
    <input v-model="text" />
    <button @click="getMovies">Cerca</button>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      text: "",
    };
  },
  methods: {
    getMovies() {
      axios.get("");
    },
  },
};
</script>

<style>
</style>