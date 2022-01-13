<template>
  <div class="row justify-content-center py-5">
    <div class="col col-5" v-for="tvShow in tvSeries" :key="tvShow.id">
      <div class="card p-3 bg-dark bg-opacity-10 mt-4">
        <h4 class="text-center">{{ tvShow.name }}</h4>
        <div class="title">
          <span>Titolo: {{ tvShow.name }}</span>
        </div>
        <div class="original_title">
          <span>Titolo originale: {{ tvShow.original_name }}</span>
        </div>
        <div class="lingua">
          <span>Lingua: {{ tvShow.original_language }}
            <flag :iso="tvShow.original_language" />
          </span>
        </div>
        <div class="voto"
          v-for="icon in 5 - Math.round(tvShow.vote_average / 2)"
          :key="icon">
          <i class="far fa-star"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tvSeries: Array,

  },
};
</script>

<style scoped lang="scss">

</style>
