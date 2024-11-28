<template>
    <div class="col-12 col-md-6 mb-4">
      <div class="card">
        <img 
          :src="poster_path ? direcimag + poster_path : 'default-poster.jpg'" 
          class="card-img-top" 
          :alt="'Poster de ' + title">
        <div class="card-body">
          <h5 class="card-title">{{ title }}</h5>
          <p class="card-text">{{ overview }}</p>
          <p class="release-date">{{ release_date }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';

  defineProps({
    poster_path: String,
    title: String,
    overview: String,
    release_date: String
  });
  
  const direcimag = 'https://image.tmdb.org/t/p/w500'; 
</script>
  