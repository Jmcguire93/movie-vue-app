<template>
  <div>
    <router-link to="/movies">Back to all movies</router-link>
    <h1>{{ movie.title }}</h1>
    <h2>{{ movie.year }}</h2>
    <h2>Directed By: {{ movie.director }}</h2>
    <p>Plot: {{ movie.plot }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">
      <button>Edit</button>
    </router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("movies/" + this.$route.params.id).then((response) => {
      this.movie = response.data;
    });
  },
};
</script>
