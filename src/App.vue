<template>
  <div id="app" class="bg-dark">
    <Header @inputSearch="callSearch" />
    <Main :films="films" :tvSeries="tvSeries" />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },

  data() {
    return {
      films: [],
      tvSeries: [],
      apiKey: "9559f92c2bc23ecddf654092232b0eb1"

    };
  },

  methods: {
    callSearch(userInput) {
      let reqMovie =
      "https://api.themoviedb.org/3/search/movie?api_key=" +
      this.apiKey +
      "&language=en-US&query=" +
      userInput;

      let reqTv =
      "https://api.themoviedb.org/3/search/tv?api_key=" +
      this.apiKey +
      "&language=en-US&query=" +
      userInput;

      const reqOne = axios.get(reqMovie);
      const reqTwo = axios.get(reqTv);
      axios
      .all([reqOne, reqTwo])
      .then(
        axios.spread((...r) => {
          this.films = r[0].data.results;
          this.tvSeries = r[1].data.results;
          console.log(this.tvSeries);
        })
      )

      .catch((e) => {
        console.log(e, "Non funziona");
      }
      );

      console.log(this.film);

    },
  },
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";

</style>
