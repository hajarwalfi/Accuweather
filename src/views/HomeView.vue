<template>
    <div class="home">
      <SearchCity @search="searchWeather" />
      <WeatherDisplay :weather="currentWeather" :error="error" />
      <ShortTermForecast :forecast="forecast" />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import SearchCity from '@/components/SearchCity.vue'
  import WeatherDisplay from '@/components/WeatherDisplay.vue'
  import ShortTermForecast from '@/components/ShortTermForecast.vue'
  
  const API_KEY = 'd2c4f254b44addc6a3ecd3cd45bb5b7d'
  const currentWeather = ref(null)
  const forecast = ref([])
  const error = ref('')
  
  const searchWeather = async (city) => {
    try {
      error.value = ''
      currentWeather.value = null
      forecast.value = []
      
      // Récupérer la météo actuelle
      const weatherResponse = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&lang=fr&appid=${API_KEY}`
      )
      
      if (!weatherResponse.ok) {
        throw new Error('Ville non trouvée. Veuillez vérifier l\'orthographe.')
      }
      
      currentWeather.value = await weatherResponse.json()
      
      // Récupérer les prévisions à court terme
      const forecastResponse = await fetch(
        `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=metric&lang=fr&appid=${API_KEY}`
      )
      
      if (forecastResponse.ok) {
        const forecastData = await forecastResponse.json()
        forecast.value = forecastData.list.slice(0, 5)
      }
    } catch (err) {
      error.value = err.message
      console.error('Erreur:', err)
    }
  }
  </script>
  
  <style scoped>
  .home {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }
  
  @media (max-width: 600px) {
    .home {
      padding: 1rem;
    }
  }
  </style>