<template>
  <div class="movie-outlet">
    <div class="search-display" v-for="movie in movies" :key="movie.imdbID"></div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      movies: [],
      searchQuery: '',
      passKey: 'bfe0cf61'
    }
  },

  methods: {
    fetchMovieData() {
      axios
        .get(`http://www.omdbapi.com/?s=${this.searchQuery}&apikey=${this.passKey}`)
        .then((response) => {
          this.movies = response.data
        })
        .catch((error) => {
          console.error('Error:', error)
        })
    }
  }
}
</script>

<style scoped>
.movie-outlet {
  padding: 1rem 2.5rem;
}
</style>
