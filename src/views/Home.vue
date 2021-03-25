<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- {{ movies }} -->
    <h3>Add a Movie</h3>
    <p>title: <input type="text" v-model="newMovieTitle"></p>
    <p>year: <input type="text" v-model="newMovieYear"></p>
    <p>plot: <input type="text" v-model="newMoviePlot"></p>
    <p>director: <input type="text" v-model="newMovieDirector"></p>
    <p>english: <input type="text" v-model="newMovieEnglish"></p>
    <button v-on:click="createMovie"> ADD</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      {{ movie.title }}
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the dark side",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
    };
  },
  created: function () {
    console.log("in created");
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      console.log("in moviesIndex");
      axios.get("http://localhost:3000/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      console.log("in create movie");
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish,
      };
      axios.post("http://localhost:3000/api/movies", params).then((response) => {
        console.log(response.data);
        this.movies.push(response.data);
      });
    },
  },
};
</script>
