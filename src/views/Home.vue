<template>
  <div class="row">
    <div class="col-md-3 ">
      <div class="card">
        <div class="card-header">
          <h5>Filter Results</h5>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md-12">
              <label for="filter_by_name" class="form-label">Name (contains)</label>
              <input type="text" id="filter_by_name" class="form-control rounded-0 border-0" placeholder="Text string" v-model="name" @keyup="searchByName">  
            </div>
            <div class="col-md-12 mt-2">
              <div class="row ">
                <div class="col-sm-4 col-md-12 ">
                  <label for="filter_by_min_score" class="form-label">Minimum Score</label>
                  <input type="number" id="filter_by_min_score" class="form-control rounded-0 border-0" v-model="min_score" @keyup="searchByMinScore">   
                </div>
                <div class="col-sm-4 col-md-12 mt-md-1 ">
                  <label for="order_by" class="form-label">Order By</label>
                  <div class="input-group">
                    <button class="input-group-text rounded-0 border-0" v-if="order_dir == 'asc'" @click="toggleOrder">
                      <i class="fa fa-arrow-up text-white"></i>
                    </button>
                    <button class="input-group-text rounded-0 border-0" v-if="order_dir == 'desc'" @click="toggleOrder">
                      <i class="fa fa-arrow-down text-white"></i>
                    </button>
                    <select id="order_by" class="form-control rounded-0 border-0" v-model="order_by" @change="orderByChanged">
                      <option value="release_date" selected>Release Date</option>
                      <option value="score">Score</option>
                      <option value="name">Name</option>
                    </select>
                  </div>
                </div>
                <div class="col-sm-4 col-md-12 mt-md-1 " v-if="filters_cleared">
                  <label for="filter_by_min_score" class="form-label">Clear Filters</label>
                  <button id="filter_by_min_score" class="form-control rounded-0 border-0 w-100 text-white" @click="clearFilters">Clear</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-md-9">
      <div v-if="error" class="mt-2">
        <div class="alert alert-danger" role="alert">
          Something went wrong, Please reload the page.
        </div>
      </div>
      <div v-if="loading" class="mt-5  text-center">
        <i class="fa fa-spinner fa-pulse fa-3x fa-fw"></i>
      </div>
      <div>
        <Game v-for="game in games" :key="game.id" v-bind:game="game"></Game>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Game from '../components/Game.vue'
// import '@ocrv/vue-tailwind-pagination/styles'

export default {
  name: 'Home',

  data() {
    return {
      games: [],
      games_unfiltered: [],
      loading: true,
      error: false,
      name: null,
      min_score: null,
      order_by: 'release_date',
      order_dir: 'asc',
      filters_cleared: false,
    };
  },

  mounted () {
    axios
      .get('https://public.connectnow.org.uk/applicant-test/')
      .then((response) => {
        this.games = response.data
        this.games_unfiltered = response.data
        this.sortByReleaseDateAsc()
      })
      .catch((error) => {
        console.log(error)
        this.error = true
      })
      .finally(() => {
        this.loading = false
      })
  },

  methods: {
    toggleOrder(){
      if (this.order_dir == 'asc') {
        this.order_dir = 'desc'
      }
      else if(this.order_dir == 'desc'){
        this.order_dir = 'asc'
      }
      this.orderByChanged()
    },
    orderByChanged(){
      if (this.order_by == 'release_date' && this.order_dir == 'asc') {
        this.sortByReleaseDateAsc()
      }
      else if(this.order_by == 'release_date' && this.order_dir == 'desc'){
        this.sortByReleaseDateDesc()
      }
      else if(this.order_by == 'score' && this.order_dir == 'asc'){
        this.sortByScoreAsc()
      }
      else if(this.order_by == 'score' && this.order_dir == 'desc'){
        this.sortByScoreDesc()
      }
      else if(this.order_by == 'name' && this.order_dir == 'asc'){
        this.sortByNameAsc()
      }
      else if(this.order_by == 'name' && this.order_dir == 'desc'){
        this.sortByNameDesc()
      }
    },
    sortByReleaseDateAsc(){
        this.games = this.games.sort((a,b) => (a.first_release_date > b.first_release_date) ? 1 : ((b.first_release_date > a.first_release_date) ? -1 : 0))
    },
    sortByReleaseDateDesc(){
        this.games = this.games.sort((a,b) => (a.first_release_date < b.first_release_date) ? 1 : ((b.first_release_date < a.first_release_date) ? -1 : 0))
    },
    sortByScoreAsc(){
        this.games = this.games.sort((a,b) => (a.rating.toFixed(0) > b.rating.toFixed(0)) ? 1 : ((b.rating.toFixed(0) > a.rating.toFixed(0)) ? -1 : 0))
    },
    sortByScoreDesc(){
        this.games = this.games.sort((a,b) => (a.rating.toFixed(0) < b.rating.toFixed(0)) ? 1 : ((b.rating.toFixed(0) < a.rating.toFixed(0)) ? -1 : 0))
    },
    sortByNameAsc(){
        this.games = this.games.sort((a,b) => (a.name > b.name) ? 1 : ((b.name > a.name) ? -1 : 0))
    },
    sortByNameDesc(){
        this.games = this.games.sort((a,b) => (a.name < b.name) ? 1 : ((b.name < a.name) ? -1 : 0))
    },
    searchByName(){
      if (this.name != null) {
        this.games = this.games.filter(item => item.name.toLowerCase().indexOf(this.name) > -1);
        this.orderByChanged()
        this.filters_cleared = true
      }
    },
    searchByMinScore(){
      if (this.min_score != null) {
        this.games = this.games.filter(item => item.rating.toFixed(0) >= this.min_score);
        this.orderByChanged()
        this.filters_cleared = true
      }
    },
    clearFilters(){
      this.games = this.games_unfiltered
      this.filters_cleared = false
      this.min_score = null
      this.name = null
      this.order_dir = 'asc'
      this.order_by = 'release_date'
    }
  },

  components: {
    'Game': Game,
  }

}
</script>
