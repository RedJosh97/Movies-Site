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
      <div class="movie-display">
        <div v-if="isLoading" class="loader-container">
          <div class="loader"></div>
          <div class="loader-text">Loading...</div>
        </div>
        <div v-if="errorMsg" class="errorNotice">{{ errorMsg }}</div>

        <div class="movie-container">
          <div class="card" v-for="movie in (moviesPost, filteredMovies)" :key="movie.id">
            <div v-if="movie.toggle" class="movie-overview">
              <p class="movie-title">{{ movie.title }}</p>
              <p class="overview-text">{{ movie.overview }}</p>
            </div>
            <img
              v-else
              :src="'https://image.tmdb.org/t/p/w200' + movie.poster_path"
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
      this.errorMsg = ''
      const searchUrl = `${this.apiUrl}/search/movie?api_key=${this.apiKey}&query=${this.searchQuery}`

      axios
        .get(searchUrl)
        .then((response) => {
          if (response.data.results.length === 0) {
            // this.errorMsg = 'movie not found'
            setTimeout(() => {
              this.errorMsg = 'movie not found'
              this.moviesPost = []
            }, 1000)
          } else {
            this.moviesPost = response.data.results
          }
          console.log('correct', response.data.results)
        })
        .catch((error) => {
          console.error('Error fetching movies:', error)
        })
        .finally(() => {
          setTimeout(() => {
            this.isLoading = false
          }, 2000)
        })
    }
  },

  computed: {
    filteredMovies() {
      return this.moviesPost.filter((movie) => movie.poster_path !== null)
    }
  }
}
</script>

<style>
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

form {
  width: 50%;
  margin: auto;
  margin-bottom: 32px;
}

.loader-container {
  background: rgba(0, 0, 0, 0.3);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.loader {
  width: 70px;
  height: 70px;
  position: relative;
}

.loader:before {
  content: '';
  width: 70px;
  height: 70px;
  border-radius: 50%;
  border: 6px solid red;
  position: absolute;
  top: 0;
  left: 0;
  animation: pulse 1s ease-in-out infinite;
}

.loader:after {
  content: '';
  width: 70px;
  height: 70px;
  border-radius: 50%;
  border: 6px solid transparent;
  border-top-color: red;
  position: absolute;
  top: 0;
  left: 0;
  animation: spin 2s linear infinite;
}

.loader-text {
  font-size: 24px;
  margin-top: 20px;
  color: red;
  font-weight: 600;
  font-family: Arial, sans-serif;
  text-align: center;
  text-transform: uppercase;
}

@keyframes pulse {
  0% {
    transform: scale(0.6);
    opacity: 1;
  }
  50% {
    transform: scale(1.2);
    opacity: 0;
  }
  100% {
    transform: scale(0.6);
    opacity: 1;
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.content {
  display: none;
}

.loaded .loader-container {
  display: none;
}

.loaded .content {
  display: block;
}
</style>
