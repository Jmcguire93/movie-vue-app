<template>
  <div class="MoviesCreate">
    <h2>Add a movie</h2>
    Title:
    <input type="text" v-model="newMovieParams.title" />
    Year:
    <input type="text" v-model="newMovieParams.year" />
    Plot:
    <input type="text" v-model="newMovieParams.plot" />
    Director:
    <input type="text" v-model="newMovieParams.director" />
    English:
    <input type="text" v-model="newMovieParams.english" />
    <button v-on:click="createMovie()">Create Movie</button>
  </div>
</template>

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

  methods: {
    createMovie: function () {
      console.log("Adding movie..");

      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
