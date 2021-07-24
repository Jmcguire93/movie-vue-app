<template>
  <div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h2>{{ movie.title }} - {{ movie.year }}</h2>
        <p>Plot: {{ movie.plot }}</p>
      </router-link>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Movies",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
      errors: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios
        .get("http://localhost:3000/movies")
        .then((response) => {
          this.movies = response.data;
          console.log("All Movies:", this.movies);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
