<template>
  <div class="container mt-4" id="Movie-app">
      <h1>Min filmlista</h1>
        <hr>
        <h2>Lägg till en film</h2>
        <form>
          <div class="form-group">
            <label for="title">Titel</label>
            <input type="input" class="form-control" id="title" placeholder="Titeln på filmen här...">
          </div>
          <label for="rating">Betyg</label>
            <select class="form-control" id="rating" >
              <option>1</option >
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option>5</option>
            </select>
        <br>
          <button type="button" class="btn btn-success">Lägg till film</button>
        </form>


        <ul id="movie-list">
          <li >
            <button id="removeBtn" class="btn btn-danger">Ta bort</button>
          </li>
        </ul>



  </div>


</template>

<script>
export default {
    data() {
        return {
        }
    },
}

</script>

<style src="./MovieList.css"> </style>