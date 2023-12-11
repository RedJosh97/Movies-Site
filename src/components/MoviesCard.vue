<template>
  <div class="movie-card">
    <video muted autoplay loop accelerometer ref="videoPlay" @click="isPlaying">
      <source :src="backgroundVideo" />
    </video>
    <div class="movie-display">
      <form @submit.prevent="searchMovies">
        <div class="search-box">
          <i class="las la-search"></i>
          <input type="text" placeholder="Search Movies" v-model="searchQuery" />
          <button class="" type="submit">Search</button>
        </div>
      </form>
      <div v-if="isLoading" class="errorNotice">...please wait</div>
      <div class="movie-display">
        <div v-if="isLoading" class="loading">Loading&#8230;</div>
        <div v-if="errorMsg" class="errorNotice">{{ errorMsg }}</div>
        <div class="movie-container">
          <div class="card" v-for="movie in moviesPost" :key="movie.id">
            <div v-if="movie.toggle" class="movie-overview">
              <p class="movie-title">{{ movie.title }}</p>
              <p class="overview-text">{{ movie.overview }}</p>
            </div>
            <img
              v-else
              :src="
                movie.poster_path
                  ? 'https://image.tmdb.org/t/p/w200' + movie.poster_path
                  : '/public/images/image not found.png'
              "
              alt="poster"
              class="image-card"
            />
            <div class="description">
              <div class="year-and-movieType">
                <button @click="toggleBtn(movie)" class="overview">overview</button>
                <p>{{ new Date(movie.release_date).getFullYear() }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      moviesPost: [],
      apiKey: '25814457dd63d4a85b7862eb51b3a95a',
      apiUrl: 'https://api.themoviedb.org/3',
      searchQuery: '',
      isLoading: false,
      playVideo: false,
      btnShow: true,
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
    },

    toggleBtn(movie) {
      movie.toggle = !movie.toggle
    },

    searchMovies() {
      this.isLoading = true
      const searchUrl = `${this.apiUrl}/search/movie?api_key=${this.apiKey}&query=${this.searchQuery}`

      axios
        .get(searchUrl)
        .then((response) => {
          if (response.data.results.length === 0) {
            this.errorMsg = 'movie not found'
            this.moviesPost = []
          } else {
            this.moviesPost = response.data.results
          }
          console.log('correct', response.data.results)
        })
        .catch((error) => {
          console.error('Error fetching movies:', error)
        })
        .finally(() => {
          this.isLoading = false
        })
    }
  }
}
</script>

<style scoped>
.movie-card {
  background: black;
}

.search-box {
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: none;
  outline: none;
  gap: 13px;
  background: #fff;
  border-radius: 14px;
}

.search-box button {
  background: red;
  color: #fff;
  height: 100%;
  padding: 3px 48px;
  border-radius: 14px;
  border: none;
  cursor: pointer;
}

.la-search {
  font-size: 2rem;
  padding-left: 8px;
}

.search-box input {
  padding: 5px 10px;
  border-radius: 14px;
  outline: none;
  width: 100%;
  font-size: 19px;
  border: none;
}

video {
  width: 100%;
  border-radius: 16px;
}

.movie-display {
  padding: 1rem 2.5rem;
}

form {
  width: 50%;
  margin: auto;
  margin-bottom: 32px;
}
</style>
