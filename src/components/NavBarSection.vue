<template>
  <div class="nav-section">
    <div class="nav-wrapper">
      <h4 class="logo-style"><span>cloud</span>9 Movies</h4>
    </div>
    <form @submit.prevent="fetchMovieData">
      <div class="search-box">
        <input type="text" placeholder="Search Movies" v-model="searchQuery" /><button
          type="submit"
        >
          Search
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'NavBarSection'
}
</script>

<style>
.nav-section {
  background: var(--primary-color);
  width: 100%;
  padding: 0.1rem 2.5rem;
  position: sticky;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.search-box {
  height: 35px;
  display: flex;
  justify-content: space-between;
  border: none;
  outline: none;
  min-width: 320px;
  gap: 13px;
  background: #fff;
  border-radius: 14px;
}

.search-box button {
  background: red;
  color: #fff;
  padding: 3px 18px;
  border-radius: 14px;
  border: none;
  cursor: pointer;
}

.search-box input {
  padding: 5px 10px;
  border-radius: 14px;
  outline: none;
  border: none;
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
