<template>
  <header>
    <div class="container">
      <h1>BOOLFLIX</h1>
      <div class="nav">
        <input type="text" v-model.trim="query" @keyup.enter="emitClick" />

        <button @click="emitClick">Cerca</button>
      </div>
    </div>
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

<style lang="scss" scoped>
header {
  background-color: black;
  padding: 20px 30px;

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    color: red;
  }
}
</style>