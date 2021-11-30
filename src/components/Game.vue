<template>
  <div class="card my-1 p-3 gradient">
    <div class="row">
      <div class="col-md-11">
        <h5 class="">{{ game.name }}</h5>
        <span class="fw-bold">Release Date: {{ new Date(game.first_release_date).toLocaleDateString() }}</span>
        <p class="mt-3">{{ game.summary }}</p>
      </div>
      <div class="col-md-1 d-flex align-items-center justify-content-center">
        <span class="badge p-3 rounded-circle bg-primary">{{ game.rating.toFixed(0) }}</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Game',

  props: {
    game: Object,
  },

  data() {
      return {
          currentPage: 1,
          perPage: 2,
          total: 20
      }
  },

}
</script>

<style >

</style>