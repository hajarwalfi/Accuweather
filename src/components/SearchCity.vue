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
  width: 100%;
  max-width: 500px;
}

.title {
  color: white;
  margin-bottom: 1.5rem;
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.3);
}

.search-box {
  display: flex;
  width: 100%;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.search-input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: none;
  font-size: 1rem;
  outline: none;
}

.search-button {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  cursor: pointer;
  font-size: 1rem;
}
  </style>
