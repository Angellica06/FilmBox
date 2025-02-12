<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import Modal from '@/components/Modal.vue';

const API_KEY = '385560baa82312c9c5a26253fbe3fca3';
const BASE_URL = 'https://api.themoviedb.org/3';
const LANGUAGE = 'pt-BR';

const movies = ref([]);
const series = ref([]);

const showModal = ref(false);
const selectedItem = ref(null);

const getPopularMovies = async () => {
  try {
    const response = await axios.get(`${BASE_URL}/movie/popular`, {
      params: { api_key: API_KEY, language: LANGUAGE },
    });
    movies.value = response.data.results.slice(0, 5);
  } catch (error) {
    console.error('Erro ao buscar filmes:', error);
  }
};

const getPopularSeries = async () => {
  try {
    const response = await axios.get(`${BASE_URL}/tv/popular`, {
      params: { api_key: API_KEY, language: LANGUAGE },
    });
    series.value = response.data.results.slice(0, 5);
  } catch (error) {
    console.error('Erro ao buscar séries:', error);
  }
};

const openModal = (item) => {
  selectedItem.value = item;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
  selectedItem.value = null;
};

onMounted(() => {
  getPopularMovies();
  getPopularSeries();
});
</script>

<template>
  <main id="home">
    <section class="banner">
      <div class="banner-content text-light">
        <h1>Explore os melhores filmes e séries</h1>
        <p>Encontre os lançamentos mais populares e descubra novas histórias incríveis.</p>
        <a class="btn" href="#movies">Comece agora <img src="../assets/img/seta-para-baixo.png"></a>
      </div>
    </section>

    <section class="container" id="movies">
      <h1 class="pt-5">Filmes Populares</h1>
      <div class="content pt-3">
        <div v-for="movie in movies" :key="movie.id" class="card" @click="openModal(movie)">
          <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title" />
          <h3 class="p-2">{{ movie.title }}</h3>
        </div>
      </div>

      <h1 class="pt-5 pb-2">Séries Populares</h1>
      <div class="content pt-3 pb-5">
        <div v-for="serie in series" :key="serie.id" class="card" @click="openModal(serie)">
          <img :src="'https://image.tmdb.org/t/p/w500' + serie.poster_path" :alt="serie.name" />
          <h3 class="p-2">{{ serie.name }}</h3>
        </div>
      </div>
    </section>
  </main>

  <Modal v-if="selectedItem" :show="showModal" :title="selectedItem.title || selectedItem.name"
    :description="selectedItem.overview || 'Descrição não disponível.'"
    :image="'https://image.tmdb.org/t/p/w500' + selectedItem.poster_path"
    :date="selectedItem.release_date || selectedItem.first_air_date" :assessment="selectedItem.vote_average"
    @closeModal="closeModal" />

  <footer class="footer text-center">
    <p>&copy; 2025 FilmBox. Todos os direitos reservados.</p>
    <div class="social-icons">
      <a href="#"><img src="../assets/icons/facebook.png" alt="Facebook"></a>
      <a href="#"><img src="../assets/icons/instagram.png" alt="Instagram"></a>
      <a href="#"><img src="../assets/icons/youtube.png" alt="YouTube"></a>
    </div>
  </footer>
</template>

<style scoped>
#home {
  scroll-margin-top: 6rem;
}

.banner {
  width: 100%;
  height: 100vh;
  background: linear-gradient(360deg, rgb(30, 25, 44) 14.95%, rgba(0, 0, 0, 0.7) 40%), url('../assets/img/banner.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin-top: 4.6rem;
}

.banner h1 {
  font-size: 3rem;
  font-weight: 700;
}

.banner p {
  font-size: 1.2rem;
}

.banner .btn {
  color: #fff718;
  border: 2px solid #fff718;
  background-color: transparent;
  font-size: 1rem;
  font-weight: 600;
  transition: all .3s ease;
}

.banner .btn:hover {
  transform: scale(1.05);
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

@media (max-width: 980px) {
  .banner {
    margin-top: 2rem;
    padding: 1rem;
  }
}
</style>
