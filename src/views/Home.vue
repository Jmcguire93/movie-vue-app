<template>
  <div class="home">
    <h2>Add a movie</h2>
    <div>
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
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" :key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More info!</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info!</h1>
        <p>Title: {{ currentMovie.title }}</p>
        <p>Year: {{ currentMovie.year }}</p>
        <p>Plot: {{ currentMovie.plot }}</p>
        <p>Director: {{ currentMovie.director }}</p>
        <p>English: {{ currentMovie.english }}</p>
        <button v-on:click="updateMovie(currentMovie)">Update!</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete!</button>
        <button>Close</button>
      </form>
    </dialog>
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
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All Movies:", this.movies);
      });
    },
    createMovie: function () {
      console.log("Adding movie..");
      // var params = {
      //   title: "School of Rock",
      //   year: 2003,
      //   plot: "Overly enthusiastic guitarist Dewey Finn (Jack Black) gets thrown out of his bar band and finds himself in desperate need of work. Posing as a substitute music teacher at an elite private elementary school, he exposes his students to the hard rock gods he idolizes and emulates -- much to the consternation of the uptight principal (Joan Cusack). As he gets his privileged and precocious charges in touch with their inner rock 'n' roll animals, he imagines redemption at a local Battle of the Bands.",
      //   director: "Richard Linklater",
      // };
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var editMovieParams = movie;
      axios.patch("http://localhost:3000/movies/" + movie.id, editMovieParams).then((response) => {
        console.log("Update successful!", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete("http://localhost:3000/movies/" + movie.id).then((response) => {
        console.log("Deleted!", response.data);
        var index = this.movie.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
