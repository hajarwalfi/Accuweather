<template>
    <div class="search-container">
      <h1 class="title">Application Météo</h1>
      <div class="search-box">
        <input 
          v-model="city" 
          @keyup.enter="searchWeather" 
          type="text" 
          placeholder="Entrez le nom d'une ville" 
          class="search-input"
        />
        <button @click="searchWeather" class="search-button">
          Rechercher
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const city = ref('')
  const emit = defineEmits(['search'])
  
  const searchWeather = () => {
    if (city.value.trim()) {
      emit('search', city.value)
    }
  }
  </script>
  
  <style scoped>
  .search-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 2rem;
  }
  
  .title {
    color: #2c3e50;
    margin-bottom: 1.5rem;
    font-size: 2rem;
  }
  
  .search-box {
    display: flex;
    width: 100%;
    max-width: 500px;
  }
  
  .search-input {
    flex: 1;
    padding: 0.75rem 1rem;
    border: 1px solid #ddd;
    border-radius: 4px 0 0 4px;
    font-size: 1rem;
  }
  
  .search-button {
    background-color: #42b883;
    color: white;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 0 4px 4px 0;
    cursor: pointer;
    font-size: 1rem;
    transition: background-color 0.3s;
  }
  
  .search-button:hover {
    background-color: #369e6f;
  }
  </style>