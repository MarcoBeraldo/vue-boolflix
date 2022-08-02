<template>
  <header>
    <input type="text" v-model.trim="query" />

    <button @click="emitClick">Cerca</button>
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

  components: {},
  methods: {
    emitClick() {
      this.$emit("search", this.query);
    },
  },
};
</script>

<style>
</style>