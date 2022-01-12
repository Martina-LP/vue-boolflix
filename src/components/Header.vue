<template>
  <header id="site-header" class="position-fixed w-100">
    <nav class="navbar navbar-light bg-dark justify-content-between">
      <a class="navbar-brand ms-5 text-primary fs-2">BOOLFLIX</a>
      <form class="d-flex me-5" v-on:submit.prevent>

        <input
          class="form-control mr-sm-2 bg-dark text-light"
          type="search"
          placeholder="Cerca film e serie tv"
          v-model="userInput"
        />

        <button
          class="btn btn-primary my-2 my-sm-0 bg-dark border-light m-1"
          type="submit"
          @click="$emit('inputSearch', userInput)"
        >
          Search
        </button>

      </form>
    </nav>
  </header>
</template>

<script>
export default {
  data() {
    return {
      userInput: "",
    };
  },
};
</script>

<style scoped lang="scss">
#site-header {
  z-index: 1000;
}
</style>
