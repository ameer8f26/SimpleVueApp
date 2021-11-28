<template>
  <div class="card my-1 p-3">
    <div class="row">
      <div class="col-md-12 ">
        <div class="float-end">
          <span class="badge p-2 align-middle float-end bg-primary">{{ game.rating.toFixed(0) }}</span>
        </div>
        <h5 class="">{{ game.name }}</h5>
        Release date: {{ new Date(game.first_release_date) }}
        <p class="mt-2">{{ game.summary }}</p>
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