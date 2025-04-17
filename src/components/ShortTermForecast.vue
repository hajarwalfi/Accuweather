<template>
    <div v-if="forecast && forecast.length > 0" class="forecast-container">
      <h3 class="forecast-title">Prévisions à court terme</h3>
      <div class="forecast-items">
        <div v-for="(item, index) in forecast" :key="index" class="forecast-item">
          <p class="forecast-time">{{ formatTime(item.dt_txt) }}</p>
          <img 
            :src="`https://openweathermap.org/img/wn/${item.weather[0].icon}.png`" 
            :alt="item.weather[0].description"
            class="forecast-icon"
          />
          <p class="forecast-temp">{{ Math.round(item.main.temp) }}°C</p>
          <p class="forecast-desc">{{ item.weather[0].description }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue'
  
  const props = defineProps({
    forecast: Array
  })
  
  const formatTime = (dateStr) => {
    const date = new Date(dateStr)
    return date.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' })
  }
  </script>
  
  <style scoped>
  .forecast-container {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    padding: 1.5rem;
    max-width: 500px;
    width: 100%;
    margin: 1.5rem auto 0;
  }
  
  .forecast-title {
    color: #2c3e50;
    margin-bottom: 1rem;
    text-align: center;
  }
  
  .forecast-items {
    display: flex;
    overflow-x: auto;
    gap: 1rem;
    padding-bottom: 0.5rem;
  }
  
  .forecast-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 80px;
    padding: 0.5rem;
    border-radius: 8px;
    background-color: #f8f9fa;
  }
  
  .forecast-time {
    font-size: 0.9rem;
    color: #7f8c8d;
    margin-bottom: 0.5rem;
  }
  
  .forecast-icon {
    width: 50px;
    height: 50px;
  }
  
  .forecast-temp {
    font-weight: bold;
    color: #2c3e50;
    margin: 0.25rem 0;
  }
  
  .forecast-desc {
    font-size: 0.8rem;
    color: #7f8c8d;
    text-align: center;
    text-transform: capitalize;
  }
  </style>