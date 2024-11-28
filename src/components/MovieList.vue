<script setup>
  import { ref, onMounted } from 'vue';
  import MovieCard from './MovieCard.vue';
  
  const contraapi = '7c63ecc439395d19ead94ec5353a34ff';
  const linkapi = 'https://api.themoviedb.org/3/movie/popular';
  const direcimag = 'https://image.tmdb.org/t/p/w500';
 
  const movies = ref([]);
  const inicio = ref(0);
  const fin = ref(5); 
  
  const getMovies = async () => {
    try {
      const response = await fetch(`${linkapi}?api_key=${contraapi}&language=es-ES&page=1`);
      const data = await response.json();
      movies.value = data.results;
    } catch (error) {
      console.error('Error al obtener datos de la API:', error);
    }
  };
  
  const nextPosts = () => {
    if (fin.value < movies.value.length) {
        inicio.value = inicio.value + 5;
        fin.value = fin.value + 5;
    }
  };
  
  const backPosts = () => {
    if (inicio.value > 0) {
        inicio.value = inicio.value - 5;
        fin.value = fin.value - 5;
    }
  };
  
  onMounted(() => {
    getMovies();
  });
</script>

<template>
    <div class="container">
      <button 
        class="btn btn-primary me-3" 
        @click="backPosts" 
        :disabled="inicio <= 0">
        Back
      </button>
      <button 
        class="btn btn-primary" 
        @click="nextPosts" 
        :disabled="fin >= movies.length">
        Next
      </button>
      
      <hr>
      
      <div class="row" id="content">
        <MovieCard 
          v-for="movie in movies.slice(inicio, fin)" 
          :key="movie.id" 
          :poster_path="movie.poster_path" 
          :title="movie.title" 
          :overview="movie.overview" 
          :release_date="movie.release_date" 
        />
      </div>
    </div>
  </template>
  