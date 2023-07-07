<template>
  <div class="weather-widget">
    <h2 class="widget-title">Widget Cuaca</h2>
    <div class="location-input">
      <label for="location">Masukkan Lokasi:</label>
      <input type="text" id="location" v-model="location" />
      <button @click="fetchWeatherData">Cek Cuaca</button>
    </div>
    <div v-if="weatherData" class="weather-data">
      <p class="location">Lokasi: {{ weatherData.name }}</p>
      <div class="current-weather">
        <p class="temperature">
          Suhu: {{ Math.round(weatherData.main.temp - 273.15) }}°C
        </p>
        <div class="weather-icon">
          <img
            :src="getWeatherIconUrl(weatherData.weather[0].icon)"
            :alt="weatherData.weather[0].description"
          />
        </div>
        <p class="description">
          Deskripsi: {{ weatherData.weather[0].description }}
        </p>
      </div>
    </div>
    <p v-else class="loading-message">Memuat....</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: '',
      weatherData: null,
    };
  },
  methods: {
    async fetchWeatherData() {
      try {
        const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        this.weatherData = data;
      } catch (error) {
        console.error('Error saat mengambil data cuaca:', error);
      }
    },
    getWeatherIconUrl(iconCode) {
      return `https://openweathermap.org/img/w/${iconCode}.png`;
    },
  },
};
</script>

<style scoped>
.weather-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #0fc7ff;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: slideIn 0.5s ease;
}

@keyframes slideIn {
  0% {
    opacity: 0;
    transform: translateY(-20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.widget-title {
  margin-top: 0;
  color: #333;
}

.location-input {
  margin-bottom: 10px;
}

.weather-data {
  margin-top: 10px;
  animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.location {
  font-size: 18px;
  font-weight: bold;
}

.current-weather {
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: slideUp 0.5s ease;
}

@keyframes slideUp {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.temperature {
  font-size: 24px;
  color: #ff5722;
  transition: color 0.3s ease;
}

.weather-icon img {
  width: 100px;
  height: 100px;
  transition: transform 0.3s ease;
}

.weather-icon:hover img {
  transform: scale(1.2);
}

.description {
  font-size: 16px;
  margin-top: 10px;
  transition: color 0.3s ease;
}

.loading-message {
  animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
