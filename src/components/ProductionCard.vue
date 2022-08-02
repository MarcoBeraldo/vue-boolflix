<template>
  <ul>
    <li>
      <img
        :src="`https://image.tmdb.org/t/p/w342${production.poster_path}`"
        alt=""
      />
    </li>
    <li>{{ title }}</li>
    <li>{{ originalTitle }}</li>
    <li>
      <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language" />
      <p v-else>{{ production.original_language }}</p>
    </li>

    <li>
      <i
        v-for="index in 5"
        class="fa-star"
        :class="
          index <= starVote(production.vote_average) ? 'fa-solid' : 'fa-regular'
        "
        :key="index"
      ></i>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ProductionCard",
  dat() {
    return {
      imgSize: "w342",
      imgUri: "https://image.tmdb.org/t/p/",
    };
  },
  props: {
    production: Object,
  },
  computed: {
    title() {
      return this.production.title || this.production.name;
    },
    originalTitle() {
      return this.production.original_title || this.production.original_name;
    },
    hasFlag() {
      const flags = ["it", "en"];
      return flags.includes(this.production.original_language);
    },
    flagSrc() {
      return require(`../assets/flags/${this.production.original_language}.png`);
    },
  },
  methods: {
    starVote(vote) {
      return Math.ceil(vote * 0.5);
    },
  },
};
</script>

<style>
</style>