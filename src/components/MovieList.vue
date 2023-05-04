<template>
  <div class="container mt-4" id="Movie-app">
      <h1>Min filmlista</h1>
        <hr>
        <h2>Lägg till en film</h2>
        <form>
          <div class="form-group">
            <label for="title">Titel</label>
            <input type="input" v-model="title" class="form-control" id="title" placeholder="Titeln på filmen här...">
          </div>
          <label for="rating">Betyg</label>
            <select class="form-control" id="rating" v-model.number="rating" >
              <option>1</option >
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option>5</option>
            </select>
        <br>
          <button type="button" class="btn btn-success"  @click="addMovie">Lägg till film</button>
        </form>

        <div v-if="showAlert" class="alert alert-warning alert-dismissible fade show" role="alert">
          <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close" @click="showAlert=false"></button>
          {{errorMessage}}
        </div>   

        <hr>
        <h2 v-if="movies.length > 0"> Dina filmer</h2>
        <ul id="movie-list">
          <li v-for="(movie, index) in movies" :key="index">
            {{ movie.title }} - 
             <span v-for="i in movie.rating" :key="i" class="star">&#9733;</span>
            <button id="removeBtn" class="btn btn-danger" @click="deleteMovie(index)">Ta bort</button>
          </li>
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
    data() {
        return {
          // Först måste vi ha en lista [] där alla filmer skall sparas i. Varje film i listan behöver också ha en titel och ett betyg. 
          movies: [],
          title: '',
          rating: '',
          showAlert: false,
          errorMessage: '',
        }
    },

    mounted: function() {
      var storedMovies = localStorage.getItem('movies');
      if (storedMovies) {
        this.movies = JSON.parse(storedMovies);
      }
    },

    methods: {
      addMovie() {
        if (this.validateUserInput()) {
          if(this.checkIfMovieExists()) {
        this.movies.push({ title: this.title, rating: this.rating });
        this.title = '';
        this.rating = '';
        localStorage.setItem('movies', JSON.stringify(this.movies));
        }
      }
      },
      deleteMovie(index){
        this.movies.splice(index, 1);
        localStorage.setItem('movies', JSON.stringify(this.movies));
      },
      sortAlphabetically(){
        this.movies.sort((a, b) => a.title.localeCompare(b.title));
      },
      sortByRating(){
        this.movies.sort((a, b) => b.rating - a.rating);
      },
      validateUserInput(){
        if (!this.title) {
          this.errorMessage = 'Fyll i titel!';
          this.showAlert = true;
          setTimeout(() => {
              this.showAlert = false;
            }, 3000);
          return false;
        }
        if (!this.rating) {
          this.errorMessage = 'Fyll i betyg!';
          this.showAlert = true;
          setTimeout(() => {
              this.showAlert = false;
            }, 3000);
          return false;
        }
        return true;
      },
      checkIfMovieExists(){
        // Kontrollera om filmen redan finns i listan
        const titleExists = this.movies.some(movie => movie.title.toLowerCase() === this.title.toLowerCase());
        if (titleExists) {
          this.errorMessage = 'Filmen finns redan i listan!';
          this.showAlert = true;
          setTimeout(() => {
              this.showAlert = false;
            }, 3000);
          return false;
        }
        return true;
      },

      
    }

}

</script>

<style src="./MovieList.css"> </style>