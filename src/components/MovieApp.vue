<template>
  <div class="container mt-4" id="Movie-app">
    <h1>Min filmlista</h1>
    <hr>
    <movie-form @add-movie="addMovie"/>
    <hr>
    <movie-list :movies="movies" @delete-movie="deleteMovie" @sort-alphabetically="sortAlphabetically" @sort-by-rating="sortByRating"/>
  </div>
</template>
  
<script>
import MovieList from './MovieList.vue';
import MovieForm from './MovieForm.vue';


export default {
  components: {
    MovieList,
    MovieForm,
  },
  data() {
    return {
      movies: [],
      showAlert: false,
      errorMessage: ''
    }
  },

  methods: {
    addMovie(movie) {
      this.movies.push(movie);
    },
    deleteMovie(index) {
      this.movies.splice(index, 1);
    },
    sortAlphabetically() {
      this.movies.sort((a, b) => a.title.localeCompare(b.title));
    },
    sortByRating() {
      this.movies.sort((a, b) => b.rating - a.rating);
    }
  }
}
</script>