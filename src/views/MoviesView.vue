<script setup>
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';

const API_KEY = '385560baa82312c9c5a26253fbe3fca3';
const BASE_URL = 'https://api.themoviedb.org/3';
const LANGUAGE = 'pt-BR';

const movies = ref([]);
const searchMovies = ref('');

const getMovies = async () => {
  try {
    const response = await axios.get(`${BASE_URL}/movie/popular`, {
      params: { api_key: API_KEY, language: LANGUAGE },
    });
    movies.value = response.data.results;
  } catch (error) {
    console.error('Erro ao buscar filmes:', error);
  }
};

const filterMovies = computed(() => {
  return movies.value.filter(movie =>
    movie.title.toLowerCase().includes(searchMovies.value.toLowerCase())
  );
})

onMounted(() => {
  getMovies();
});
</script>

<template>
  <main class="movies">
    <section class="container">
      <div class="search">
        <input class="p-1 rounded-3" v-model="searchMovies" type="search" placeholder="Buscar por filme">
      </div>
      <div class="content pt-3">
        <p v-if="filterMovies.length === 0">Nenhum filme encontrado. 🔍</p>
        <div v-for="movie in filterMovies" :key="movie.id" class="card">
          <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title" />
          <h3 class="p-2">{{ movie.title }}</h3>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.movies {
  padding-top: 4.8rem;
  min-height: 100vh;
}

.container {
  text-align: center;
  padding: 1rem;
  color: #fff718;
}

.content {
  display: flex;
  flex-wrap: wrap;
  gap: 1.4rem;
  justify-content: center;
}
</style>
