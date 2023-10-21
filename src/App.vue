<template>
  <div>
    <NavBarSection />
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
  components: {
    NavBarSection,
    FooterSection,
    MoviesCard,
    MovieOutlet
  }
}
</script>

<style scoped></style>
