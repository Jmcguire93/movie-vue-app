<template>
  <div class="movie-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="editMovieParams.year" />
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="editMovieParams.director" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="editMovieParams.plot" />
      </div>
      <input type="submit" value="Submit" />
    </form>
    <button v-on:click="destroyMovie">Delete Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      editMovieParams: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.editMovieParams = response.data;
    });
  },
  methods: {
    updatemovie: function () {
      axios.patch("/movies/" + this.$route.params.id, this.editMovieParams).then((response) => {
        console.log(response.data);
        this.$router.push("/movies/" + response.data.id);
      });
    },
    destroyMovie: function () {
      axios.delete("/movies/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>
