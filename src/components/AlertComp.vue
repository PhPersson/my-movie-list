<template>
  <transition name="alert-fade">
    <div v-if="showAlert" class="alert alert-danger alert-dismissible fade show" role="alert">
      <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close" @click="showAlert = false"></button>
      {{ errorMessage }}
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    errorMessage: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      showAlert: true,
    };
  },
};
</script>