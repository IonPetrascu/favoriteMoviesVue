<template>
  <main>
<header class="header">
  <img class="header-logo" src="/logo.svg" alt="logo">
  <h3>My favorite Movies</h3>
  </header>
  <div class="tabs">
    <button @click="setTab(1)" :class="['btn',{btn_green:movieStore.activeTab === 1}]">Favorite</button>
    <button @click="setTab(2)" :class="['btn',{btn_green:movieStore.activeTab === 2}]">Search</button>
  </div>
  <div v-if="movieStore.activeTab === 1" class="movies">
    <div>
      <h3>Watched Movies (count : {{ movieStore.watchedMovies.length }})</h3>
    <Movie v-for="movie of movieStore.watchedMovies" :movie="movie" :key="movie.id"/>
    </div>
    <h3>All Movies (count : {{ movieStore.totalCountMovies }})</h3>
    <Movie v-for="movie of movieStore.movies" :movie="movie" :key="movie.id"/>
  </div>
  <div v-else class="search">
    <Search/>
  </div>
  </main>

</template>

<script setup>
import Search from './components/Search.vue'
import Movie from './components/Movie.vue'
import {useMovieStore} from './stores/MovieStore'


const movieStore = useMovieStore()
const setTab = (id)=>{
  movieStore.setActiveTab(id)
}

</script>




<style  lang="css">
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
.header-logo {
  max-width: 50px;
  margin-right: 10px;
}
.btn {
  border: none;
  width: 100px;
  height: 40px;
  font-size: 14px;
  margin: 0 10px;
  border-radius: 10px;
  cursor: pointer;
  background: #efefef;
}
.btn:hover {
  opacity: 0.7;
}
.btn_green {
  background: #37df5c;
}

.tabs {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}
</style>import { useMovieStore } from './stores/MovieStore';useMovieStore,
