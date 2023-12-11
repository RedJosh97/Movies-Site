<template>
  <div class="nav-section">
    <div class="nav-wrapper">
      <h4 class="logo-style"><span>cloud</span>9 Movies</h4>
    </div>
    <!-- <form @submit.prevent="fetchMovieData">
      <div class="search-box">
        <input type="text" placeholder="Search Movies" v-model="searchQuery" /><button
          type="submit"
        >
          Search
        </button>
      </div>
    </form> -->
  </div>
</template>

<script>
export default {
  name: 'NavBarSection',

  data() {
    return {
      //   movies: [],
      //   apiKey: '25814457dd63d4a85b7862eb51b3a95a',
      //   apiUrl: 'https://api.themoviedb.org/3',
      //   searchQuery: 'kill'
    }
  }
}

//   methods: {
//     searchMovies() {
//       const searchUrl = `${this.apiUrl}/search/movie?api_key=${this.apiKey}&query=${this.searchQuery}`

//       axios
//         .get(searchUrl)
//         .then((response) => {
//           console.log('achieve', response.data.results)
//         })
//         .catch((error) => {
//           console.error('Error fetching movies:', error)
//         })
//     }
//   }
// }
</script>

<style>
.nav-section {
  background: var(--primary-color);
  padding: 0.1rem 2.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-style {
  color: #fff;
  font-size: 2rem;
  font-family: var(--style-font);
}
span {
  font-size: 1.5rem;
  margin-right: -3px;
  color: red;
}

.search-btn {
  padding: 9px;
  outline: none;
  border: none;
  min-width: 230px;
  border-radius: 9px;
}
</style>
