<template>
  <div class="movie">
    <img
      :src="`https://image.tmdb.org/t/p/w300_and_h450_bestv2${movie.poster_path}`"
      :alt="movie.original_title"
      class="movie-img" />
    <div>
      <div class="movie-name">
        {{ movie.original_title }} ({{ movie.release_date }})
      </div>
      <span class="movie-overview">{{ movie.overview }}</span>
      <div v-if="!isSearch" class="movie-buttons">
        <button @click="movieStore.toggleWatched(movie.id)" class="btn movie-buttons-watched">
          <span v-if="!movie.isWatched">Watched</span>
          <span v-else>Unwatched</span>
        </button>
        <button @click="movieStore.deleteMovie(movie.id)" class="btn movie-buttons-delete">Delete</button>
      </div>
      <div v-else class="movie-buttons">
        <button @click="searchStore.addToUserMovies(movie)" class="btn btn_green">
          Add
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useMovieStore } from '@/stores/MovieStore';
import { useSearchStore } from '@/stores/SearchStore';
const movieStore = useMovieStore()
const searchStore = useSearchStore()
const props = defineProps({
  movie:{
    type:Object,
    require:true,
    default:()=>{}
  },
  isSearch:{
    type:Boolean,
    required:false,
    default:false
  }
})

</script>

<style lang="css" scoped>
.movie {
  display: grid;
  grid-template-columns: 200px 1fr;
  column-gap: 30px;
  margin-bottom: 20px;
  border: 2px solid #efefef;
  padding: 10px;
  border-radius: 10px;
}

.movie-accept {
  margin-right: 10px;
}

.movie-img {
  width: 200px;
  height: 200px;
  object-fit: cover;
  border-radius: 50%;
}

.movie-name {
  display: flex;
  align-items: center;
  font-size: 20px;
  margin-bottom: 20px;
}

.movie-overview {
  display: block;
  margin-bottom: 20px;
}

.movie-buttons {
  display: flex;
  align-items: center;
  justify-content: center;
}

.movie-buttons-watched {
  color: #fff;
  background: #1eb4c3;
}

.movie-buttons-watched__icon {
  width: 15px;
  margin-left: 10px;
}

.movie-buttons-delete {
  color: #fff;
  background: #ff2a2a;
}
</style>import { useSearchStore } from '@/stores/SearchStore';
