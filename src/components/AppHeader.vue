<template>
  <header>
    <input v-model="query" />

    <button @click="emitClick">Cerca</button>
  </header>
</template>

<script>
export default {
  name: "AppHeader",

  components: {},
  methods: {
    emitClick() {
      this.$emit("clicked-search");
    },
  },
};
</script>

<style>
</style>