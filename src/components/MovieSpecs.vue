<template>
  <div class="row justify-content-center py-5">
    <div class="col" v-for="film in films" :key="film.id">
      <div class="card bg-dark mt-4">
        <div class="testo text-primary">
          <h4 class="text-center">{{ film.title }}</h4>
          <div class="title">
            <span>Titolo: {{ film.title }}</span>
          </div>
          <div class="original_title">
            <span>Titolo originale: {{ film.original_title }}</span>
          </div>
          <div class="language">
            <span>Lingua: {{ film.original_language }}
              <flag :iso="'gb'" v-if="film.original_language == 'en'" />
              <flag :iso="film.original_language" v-else />
            </span>
          </div>
          <div class="voto">
            <!-- <i class="fas fa-star text-warning"
              v-for="icon in parseInt((film.vote_average / 2).toFixed(0))"
              :key="icon"></i> -->
            <i class="fas fa-star text-warning"
              v-for="icon in Math.round(film.vote_average / 2)"
              :key="icon"></i>
            <!-- <i class="far fa-star text-warning"
              v-for="icon in parseInt(5 - (film.vote_average / 2).toFixed(0))"
              :key="icon.id"></i> -->
            <i class="far fa-star text-warning"
              v-for="icon in 5 - Math.round(film.vote_average / 2)"
              :key="icon.id"></i>
          </div>
          <div class="overview">
            <p v-if="film.overview.length > 180">
              Overview:
              {{ film.overview.substring(-1, 300) + "..." }}
            </p>
            <p v-else>
              Overview:
              {{ film.overview }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <hr class="text-light" />
    <div class="col" v-for="tvSerie in tvSeries" :key="tvSerie.id">
      <div class="card bg-dark mt-4">
        <div class="testo text-primary">
          <h4 class="text-center">{{ tvSerie.name }}</h4>
          <div class="title">
            <span>Titolo: {{ tvSerie.name }}</span>
          </div>
          <div class="original_title">
            <span>Titolo originale: {{ tvSerie.original_name }}</span>
          </div>
          <div class="language">
            <span>Lingua: {{ tvSerie.original_language }}
              <flag :iso="tvSerie.original_language" />
            </span>
          </div>
          <div class="voto">
            <i class="fas fa-star text-warning"
              v-for="icon in Math.round(tvSerie.vote_average / 2)"
              :key="icon.id"></i>
            <i class="far fa-star text-warning"
              v-for="icon in 5 - Math.round(tvSerie.vote_average / 2)"
              :key="icon"></i>
          </div>
          <div class="overview">
            <p v-if="tvSerie.overview.length > 180">
              Overview:
              {{ tvSerie.overview.substring(-1, 300) + "..." }}
            </p>
            <p v-else>
              Overview:
              {{ tvSerie.overview }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    films: Array,
  
  },
};
</script>

<style scoped lang="scss">
.col {
  min-width: 300px;

  .card {
    position: relative;
    cursor: pointer;
    border: none;

    .testo {
      position: absolute;
      width: 300px;
      padding: 16px;
      text-align: center;
    }
  }
}
</style>
