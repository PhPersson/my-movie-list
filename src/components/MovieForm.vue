<template>
  <div>
    <h2>Lägg till en film</h2>
    <form>
      <div class="form-group">
        <label for="title">Titel</label>
        <input type="input" v-model="title" class="form-control" id="title" placeholder="Titeln på filmen här...">
      </div>
      <label for="rating">Betyg</label>
      <select class="form-control" id="rating" v-model.number="rating">
        <option>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
      </select>
      <br>
      <button type="button" class="btn btn-success" @click="addMovie">Lägg till film</button>
    </form>

    <transition name="alert-fade">
      <div v-if="showAlert" class="alert alert-warning alert-dismissible fade show" role="alert">
        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close" @click="showAlert=false"></button>
        {{errorMessage}}
      </div>
    </transition>
  </div>
</template>
  
<script>
  export default {

    data() {
      return {
        title: '',
        rating: '',
        showAlert: false,
        errorMessage: ''
      }
    },
    methods: {
      addMovie() {
        if (this.validateUserInput()) {
            this.$emit('add-movie', {
              title: this.title,
              rating: this.rating
            });
          this.title = '';
          this.rating = '';
        }
      },
      validateUserInput() {
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
    }
  }
</script>
  