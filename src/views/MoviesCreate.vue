<template>
  <div>
    <form v-on:submit.prevent="createMovie()">
      <h1>Add a Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
        <!-- <small>{{ 20 - newMovieParams.title.length }} characters remaining</small> -->
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <small>{{ 300 - newMovieParams.plot.length }} characters remaining</small>
      </div>
      <div>
        <label>English?:</label>
        <input type="checkbox" value="true" v-model="newMovieParams.english" />
      </div>
      <input type="submit" value="Submit" />
    </form>
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
