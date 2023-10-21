<!-- <template>
  <div class="movie-outlet">
    <div class="movie-container">
      <div
        class="card"
        v-for="movie in grabMovies"
        :key="movie.imdbID"
        :class="{ 'movie-card': movie.Type === 'movie', 'series-card': movie.Type === 'series' }"
      >
        <img :src="movie.Poster" alt="poster" class="image-card" />
        <p class="movie-title">{{ movie.Title }}</p>
        <div class="description">
          <p>{{ movie.Type }}</p>
          <p>{{ movie.Year }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MovieOutlet',

  data() {
    return {
      grabMovies: []
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      axios
        .get('http://www.omdbapi.com/?s=movies&apikey=bfe0cf61')
        .then((res) => {
          this.grabMovies = res.data.Search
        })
        .catch((error) => {
          console.error('Error:', error)
        })
    }
  }
}
</script> -->

<template>
  <div class="movie-outlet">
    <h4>Media</h4>
    <div class="movie-container">
      <div
        class="card"
        v-for="movie in grabMovies"
        :key="movie.imdbID"
        :class="{ 'movie-card': movie.Type === 'movie', 'series-card': movie.Type === 'series' }"
      >
        <!-- <img :src="movie.Poster" alt="poster" class="image-card" /> -->
        <p class="movie-title">{{ movie.Title }}</p>
        <div class="description">
          <p>{{ movie.Type }}</p>
          <p>{{ movie.Year }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MovieOutlet',
  data() {
    return {
      grabMovies: []
    }
  },

  mounted() {
    this.fetchData()
  },

  methods: {
    fetchData() {
      axios
        .get('http://www.omdbapi.com/?s=series&apikey=bfe0cf61')
        .then((res) => {
          this.grabMovies = res.data.Search
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
  background-color: lightblue;
}

.series-card {
  background-color: lightgreen;
}
.movie-outlet {
  padding: 1rem 2.5rem;
  background: var(--secondary-color);
}

.movie-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 35px;
  align-items: center;
  margin-top: 2rem;
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
  height: 290px;
  min-width: 210px;
  width: 20%;
  object-fit: cover;
  position: relative;
}

.card .movie-title {
  display: flex;
  align-self: flex-end;
}

.card .description {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  background: var(--primary-color);
  width: 100%;
  height: 45px;
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

.card .movie-title {
  font-weight: bolder;
  text-align: center;
  display: flex;
  justify-content: center;
  color: var(--secondary-color);
}
</style>
