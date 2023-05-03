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


        <ul id="movie-list">
          <li v-for="(movie, index) in movies" :key="index">
            {{ movie.title }} - 
            <button id="removeBtn" class="btn btn-danger">Ta bort</button>
          </li>
        </ul>



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
        }
    },

    methods: {
      addMovie() {
        if (!this.title) {
          alert("Fyll i titel!");
          return;
        }
        if (!this.rating) {
          alert("Fyll i betyg!");
          return;
        }
        this.movies.push({ title: this.title, rating: this.rating });
        this.title = '';
        this.rating = '';

      },
    }

}

</script>

<style src="./MovieList.css"> </style>