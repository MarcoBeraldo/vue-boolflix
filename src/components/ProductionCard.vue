<template>
  <div class="card-container">
    <div class="card">
      <div class="front-side">
        <img
          class="movie-poster"
          v-if="production.poster_path"
          :src="`https://image.tmdb.org/t/p/w342${production.poster_path}`"
        />
        <img
          class="alt-img"
          v-else
          src="../assets/imgmiss.png"
          alt="Poster not available"
        />
      </div>
      <div class="back-side">
        <ul>
          <li><b>Titolo: </b> {{ title }}</li>
          <li><b>Titolo originale: </b>{{ originalTitle }}</li>
          <li>
            <span><b>Lingua:</b></span>
            <img
              class="flag-img"
              v-if="hasFlag"
              :src="flagSrc"
              :alt="production.original_language"
            />
            <p v-else>{{ production.original_language }}</p>
          </li>

          <li>
            <i
              v-for="index in 5"
              class="fa-star"
              :class="
                index <= starVote(production.vote_average)
                  ? 'fa-solid'
                  : 'fa-regular'
              "
              :key="index"
            ></i>
          </li>
          <li class="overview">{{ production.overview }}</li>
        </ul>
      </div>
    </div>
  </div>
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

<style lang="scss" scoped>
.card-container {
  width: 342px;
  height: 513px;
  perspective: 1000px;
  margin: 2rem;
  font-size: 1.2rem;
}
.card {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 1s;
}
.front-side,
.back-side {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.back-side {
  transform: rotateY(180deg);
  background-color: black;
  color: white;
  padding: 20px;
}

.card-container:hover .card {
  transform: rotateY(180deg);
}

.movie-poster {
  width: 100%;
  height: 100%;
}

ul {
  list-style-type: none;
}

li.overview {
  overflow-y: auto;
  max-height: 250px;
  padding: 3px;
}

.flag-img {
  height: 20px;
  margin-left: 10px;
}

/* width */
::-webkit-scrollbar {
  width: 7px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}

li {
  margin: 15px 0;
}

.fa-star {
  color: yellow;
}

.fa-regular.fa-star {
  color: white;
}

.alt-img {
  height: 100%;
  width: 100%;
}
</style>