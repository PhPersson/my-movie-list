<template>
  <div>
    <h2 v-if="movies.length > 0">Dina filmer</h2>
    <ul id="movie-list">
      <transition-group name="fade">
        <li v-for="(movie, index) in movies" :key="index">
          {{ movie.title }} -
          <span v-for="i in movie.rating" :key="i" class="star">&#9733;</span>
          <button id="removeBtn" class="btn btn-danger" @click="deleteMovie(index)">Ta bort</button>
        </li>
      </transition-group>
    </ul>

      <button v-if="movies.length > 1" id="order-alphabetic" class="btn btn-primary" @click="sortAlphabetically">
          Alfabetisk ordning A-Z
      </button>
      <button v-if="movies.length > 1" id="order-grade" class="btn btn-primary" @click="sortByRating">
          Betygsordning
      </button>
  </div>
</template>
  
<script>
  export default {
    props: {
      movies: {
        type: Array,
        required: true
      }
    },
    methods: {
      deleteMovie(index) {
        this.$emit('delete-movie', index);
      },
      sortAlphabetically() {
        this.$emit('sort-alphabetically');
      },
      sortByRating() {
        this.$emit('sort-by-rating');
      }
    }
  }
</script>

<style>
    #movie-list > li {
    list-style: none;
    background-color: #eee;
    margin: 5px;
    padding: 20px;
    align-items: center;
    box-shadow: 0 0 5px #999;
    }

    #movie-list > li > #removeBtn{
    float: right;
    margin-left: 5px;
    }

    #movie-list > li > .star {
    color: gold;
    }

    .delete-movie {
    align-items: center;
    }

    .fade-enter-active, .fade-leave-active {
    transition: all 1s ease;
    }
    .fade-enter-from, .fade-leave-to {
    opacity: 0;
    }

</style>