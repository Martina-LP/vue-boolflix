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
        <img
          src="data:image/png;base64,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"
          alt=""
          v-if="film.poster_path == null"
          class="image" />
        <img
          v-else
          :src="`https://image.tmdb.org/t/p/w342` + film.poster_path"
          alt=""
          class="image" />
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
        <img
          src="data:image/png;base64,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"
          alt=""
          v-if="tvSerie.poster_path == null"
          class="image" />
        <img
          v-else
          :src="`https://image.tmdb.org/t/p/w342` + tvSerie.poster_path"
          alt=""
          class="image" />
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

    .image {
      object-fit: cover;
      object-position: top;
      height: 450px;
      width: 300px;
      z-index: 2;
      &:hover {
        filter: opacity(0.05);
        transition: 1s;
      }
    }

    .testo {
      position: absolute;
      width: 300px;
      padding: 16px;
      text-align: center;
    }
  }
}
</style>
