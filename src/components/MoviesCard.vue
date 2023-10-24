<template>
  <div class="movie-card">
    <video muted autoplay loop accelerometer ref="videoPlay" @click="isPlaying">
      <source :src="backgroundVideo" />
    </video>
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
      playVideo: false,
      backgroundVideo:
        '/public/images/Mission_ Impossible – Dead Reckoning Part One _ Official Trailer (2023 Movie) - Tom Cruise.mp4'
    }
  },

  methods: {
    isPlaying() {
      const video = this.$refs.videoPlay

      if (this.playVideo) {
        video.pause()
      } else {
        video.play()
      }
      this.playVideo = !this.playVideo
    }
  },

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
