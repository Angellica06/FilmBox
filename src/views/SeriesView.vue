<script setup>
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';
import Modal from '@/components/Modal.vue';

const API_KEY = '385560baa82312c9c5a26253fbe3fca3';
const BASE_URL = 'https://api.themoviedb.org/3';
const LANGUAGE = 'pt-BR';

const series = ref([]);
const searchSeries = ref('');
const selectedSerie = ref(null);
const showModal = ref(false);

const getSeries = async () => {
  try {
    const response = await axios.get(`${BASE_URL}/tv/popular`, {
      params: { api_key: API_KEY, language: LANGUAGE },
    });
    series.value = response.data.results;
  } catch (error) {
    console.error('Erro ao buscar séries:', error);
  }
};

const filterSeries = computed(() => {
  return series.value.filter(serie =>
    serie.name.toLowerCase().includes(searchSeries.value.toLowerCase())
  );
});

const openModal = (serie) => {
  selectedSerie.value = serie;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};

onMounted(() => {
  getSeries();
});
</script>

<template>
  <main class="series">
    <section class="container">
      <div class="search">
        <input class="p-1 rounded-3" v-model="searchSeries" type="search" placeholder="Buscar por Série">
      </div>
      <div class="content pt-3">
        <p v-if="filterSeries.length === 0">Nenhuma série encontrada. 🔍</p>
        <div v-for="serie in filterSeries" :key="serie.id" class="card" @click="openModal(serie)">
          <img :src="'https://image.tmdb.org/t/p/w500' + serie.poster_path" :alt="serie.name" />
          <h3 class="p-2">{{ serie.name }}</h3>
        </div>
      </div>
    </section>

    <Modal v-if="showModal" :show="showModal" :title="selectedSerie.name"
      :description="selectedSerie.overview || 'Descrição não disponível.'"
      :image="'https://image.tmdb.org/t/p/w500' + selectedSerie.poster_path" :date="selectedSerie.first_air_date"
      :assessment="selectedSerie.vote_average" @closeModal="closeModal">
    </Modal>
  </main>
</template>

<style scoped>
.series {
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