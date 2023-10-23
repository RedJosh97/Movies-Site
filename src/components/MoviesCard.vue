<template>
  <div class="movie-card">
    <video muted loop allowfullscreen>
      <source :src="watch" />
    </video>
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
      pageNumber: 3,
      passKey: 'bfe0cf61',
      watch: '/public/images/THE_CHANNEL_Official_Trailer_(2023)(720p).mp4'
    }
  },

  methods: {
    fetchMovieData() {
      axios
        .get(
          `http://www.omdbapi.com/?s=${this.searchQuery}&apikey=${this.passKey}?page=${this.pageNumber}`
        )
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
.movie-card {
  height: 100vh;
  background: black;
}

video {
  width: 100%;
  height: 100vh;
  border-radius: 16px;
}
</style>
