<template>
  <main>
    <div class="container">
      <MovieSpecs :films="films" :tvSeries="tvSeries" />
      <hr />
      <hr />
      <!-- <TvSpecs :tvSeries="tvSeries" /> -->
    </div>
  </main>
</template>

<script>
import MovieSpecs from "./MovieSpecs.vue";
// import TvSpecs from "./TvSpecs.vue";

export default {
  components: {
    MovieSpecs,
    // TvSpecs,
  },
  props: {
    films: Array,
    tvSeries: Array,
  },
  mounted() {},
  methods: {},
};
</script>

<style scoped lang="scss">

</style>
