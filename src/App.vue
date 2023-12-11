<template>
  <div v-if="loadingState" class="loader-container load">
    <div class="loader"></div>
    <div class="loader-text">Loading...</div>
  </div>

  <NavBarSection />
  <div class="app">
    <MoviesCard />
    <MovieOutlet />
    <FooterSection />
  </div>
</template>

<script>
import NavBarSection from './components/NavBarSection.vue'
import FooterSection from './components/FooterSection.vue'
import MoviesCard from './components/MoviesCard.vue'
import MovieOutlet from './components/MovieOutlet.vue'

export default {
  data() {
    return {
      loadingState: true
    }
  },
  components: {
    NavBarSection,
    FooterSection,
    MoviesCard,
    MovieOutlet
  },

  mounted() {
    this.loadingState = true
    setTimeout(() => {
      this.loadingState = false
    }, 500)
  }
}
</script>

<style scoped>
.app {
  max-width: 1440px;
  margin: auto;
}
</style>
