<template>
  <div class="movie-outlet">
    <h4>Popular Collection</h4>
    <div v-if="errorMsg" class="errorNotice">{{ errorMsg }}</div>
    <div v-else class="movie-container">
      <div class="card" v-for="movie in listedMoviesToDisplay" :key="movie.id">
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
    <button v-if="showBtn" @click="moreMovieSlide" class="more-item">More Movies</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MovieOutlet',
  data() {
    return {
      grabMovies: [],
      apiKey: '25814457dd63d4a85b7862eb51b3a95a',
      apiUrl: 'https://api.themoviedb.org/3',
      errorMsg: null,
      movieCount: 8
    }
  },

  mounted() {
    this.fetchData()
  },

  computed: {
    listedMoviesToDisplay() {
      return this.grabMovies.slice(0, this.movieCount)
    },

    otherMovies() {
      return this.grabMovies.slice(this.movieCount)
    },

    showBtn() {
      return this.otherMovies.length > 0
    }
  },

  methods: {
    toggleBtn(movie) {
      movie.toggle = !movie.toggle
    },

    moreMovieSlide() {
      this.movieCount += 8
    },

    fetchData() {
      axios
        .get(`${this.apiUrl}/movie/popular?api_key=${this.apiKey}`)
        .then((res) => {
          this.grabMovies = res.data.results
        })
        .catch((error) => {
          this.errorMsg = 'Bad request: ' + error.message
        })
    }
  }
}
</script>

<style>
.errorNotice {
  color: #fff;
  font-size: 31px;
}

.movie-overview {
  padding: 9px;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}

.movie-overview .movie-title:hover {
  color: #fff !important;
}

.overview {
  cursor: pointer;
  padding: 4px;
  background: red;
  outline: none;
  border: none;
  border-radius: 5px;
  color: #fff;
}

.overview:hover {
  opacity: 0.8;
}
.movie-outlet {
  padding: 1rem 2.5rem;
  background: var(--secondary-color);
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 60px;
}

.movie-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 40px;
  align-items: center;
}

.movie-outlet h4 {
  font-family: var(--header);
  font-size: 32px;
  color: #fff;
  text-shadow: 0 2px 9px red;
}

.movie-container .card {
  background: rgb(235, 229, 229);
  border-radius: 14px;
  height: 300px;
  min-width: 250px;
  position: relative;
}

.card:hover {
  background: var(--primary-color);
}

.more-item:hover {
  opacity: 0.9;
}

.more-item {
  padding: 14px;
  border-radius: 13px;
  background: #fff;
  border: none;
  outline: none;
  font-weight: 600;
  font-size: 1rem;
  color: red;
  box-shadow: 0 2px 9px red;
  cursor: pointer;
}

.movie-title,
.overview-text {
  padding-bottom: 5px;
  border-bottom: 2px solid var(--secondary-color);
  font-weight: bolder;
  color: red;
  text-align: center;
}

.movie-title:hover,
.movie-year:hover {
  color: green;
}

.year-and-movieType {
  display: flex;
  justify-content: space-between;
}

.card .description {
  justify-content: space-between;
  align-items: center;
  position: absolute;
  background: var(--primary-color);
  width: 100%;
  padding: 13px;
  bottom: 0;
  left: 0;
  right: 0;
}
.card .description p {
  color: #fff;
  font-weight: 800;
}

.card .image-card {
  width: 100%;
  height: 100%;
  border-radius: 12px;
}
</style>
