<template>
  <div class="row justify-content-center py-5">
    <div class="col col-5" v-for="tvSerie in tvSeries" :key="tvSerie.id">
      <div class="card p-3 bg-dark bg-opacity-10 mt-4">
        <h4 class="text-center">{{ tvSerie.name }}</h4>
        <div class="title">
          <span>Titolo: {{ tvSerie.name }}</span>
        </div>
        <div class="original_title">
          <span>Titolo originale: {{ tvSerie.original_name }}</span>
        </div>
        <div class="lingua">
          <span>Lingua: {{ tvSerie.original_language }}
            <flag :iso="tvSerie.original_language" />
          </span>
        </div>
        <div class="voto"
          v-for="icon in 5 - Math.round(tvSerie.vote_average / 2)"
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
