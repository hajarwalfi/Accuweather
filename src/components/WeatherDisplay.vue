<template>
    <div v-if="weather" class="weather-container">
      <div class="weather-header">
        <h2 class="city-name">{{ weather.name }}, {{ weather.sys.country }}</h2>
        <p class="date">{{ formattedDate }}</p>
      </div>
      
      <div class="weather-info">
        <div class="temperature">
          <span class="temp-value">{{ Math.round(weather.main.temp) }}°C</span>
          <div class="temp-details">
            <p>Min: {{ Math.round(weather.main.temp_min) }}°C</p>
            <p>Max: {{ Math.round(weather.main.temp_max) }}°C</p>
          </div>
        </div>
        
        <div class="weather-description">
          <img 
            :src="`https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`" 
            :alt="weather.weather[0].description"
            class="weather-icon"
          />
          <p>{{ weather.weather[0].description }}</p>
        </div>
      </div>
      
      <div class="weather-details">
        <div class="detail-item">
          <p class="detail-label">Humidité</p>
          <p class="detail-value">{{ weather.main.humidity }}%</p>
        </div>
        <div class="detail-item">
          <p class="detail-label">Vent</p>
          <p class="detail-value">{{ Math.round(weather.wind.speed * 3.6) }} km/h</p>
        </div>
        <div class="detail-item">
          <p class="detail-label">Pression</p>
          <p class="detail-value">{{ weather.main.pressure }} hPa</p>
        </div>
      </div>
    </div>
    <div v-else-if="error" class="error-message">
      {{ error }}
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  
  const props = defineProps({
    weather: Object,
    error: String
  })
  
  const formattedDate = computed(() => {
    if (!props.weather) return ''
    
    const date = new Date()
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' }
    return date.toLocaleDateString('fr-FR', options)
  })
  </script>
  
  <style scoped>
  .weather-container {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    padding: 1.5rem;
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
  }
  
  .weather-header {
    margin-bottom: 1.5rem;
    text-align: center;
  }
  
  .city-name {
    font-size: 1.8rem;
    margin-bottom: 0.5rem;
    color: #2c3e50;
  }
  
  .date {
    color: #7f8c8d;
    font-size: 1rem;
  }
  
  .weather-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1.5rem;
  }
  
  .temperature {
    display: flex;
    flex-direction: column;
  }
  
  .temp-value {
    font-size: 3rem;
    font-weight: bold;
    color: #2c3e50;
  }
  
  .temp-details {
    color: #7f8c8d;
    font-size: 0.9rem;
  }
  
  .weather-description {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-transform: capitalize;
  }
  
  .weather-icon {
    width: 80px;
    height: 80px;
  }
  
  .weather-details {
    display: flex;
    justify-content: space-between;
    background-color: #f8f9fa;
    border-radius: 8px;
    padding: 1rem;
  }
  
  .detail-item {
    text-align: center;
    flex: 1;
  }
  
  .detail-label {
    color: #7f8c8d;
    font-size: 0.9rem;
    margin-bottom: 0.25rem;
  }
  
  .detail-value {
    font-weight: bold;
    color: #2c3e50;
  }
  
  .error-message {
    color: #e74c3c;
    text-align: center;
    padding: 1rem;
    background-color: #fadbd8;
    border-radius: 8px;
    max-width: 500px;
    margin: 0 auto;
  }
  </style>