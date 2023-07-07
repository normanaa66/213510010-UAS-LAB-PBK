<template>
    <div class="location-widget">
      <h2>Lokasi Anda</h2>
      <div v-if="latitude && longitude">
        <p>Latitude: {{ latitude }}</p>
        <p>Longitude: {{ longitude }}</p>
      </div>
      <div v-else>
        <p>Mencari Lokasi Anda...</p>
      </div>
  
      <div class="location-input">
        <label for="latitude">Latitude:</label>
        <input type="text" id="latitude" v-model="inputLatitude" />
      </div>
      <div class="location-input">
        <label for="longitude">Longitude:</label>
        <input type="text" id="longitude" v-model="inputLongitude" />
      </div>
  
      <button @click="fetchLocationDetails">Mencari...</button>
  
      <div v-if="foundLocation" class="location-details">
        <h3>Location Details</h3>
        <p>Country: {{ foundLocation.components.country }}</p>
        <p>City: {{ foundLocation.components.city }}</p>
        <p>Street: {{ foundLocation.components.street }}</p>
        <p>Postal Code: {{ foundLocation.components.postcode }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        latitude: null,
        longitude: null,
        inputLatitude: '',
        inputLongitude: '',
        foundLocation: null,
      };
    },
    mounted() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.getPosition);
      }
    },
    methods: {
      getPosition(position) {
        this.latitude = position.coords.latitude;
        this.longitude = position.coords.longitude;
      },
      async fetchLocationDetails() {
        try {
          const apiKey = '92591005a7b94008909d59a64b6d2a49';
          const latitude = this.inputLatitude || this.latitude;
          const longitude = this.inputLongitude || this.longitude;
          const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
            latitude + ',' + longitude
          )}&key=${apiKey}`;
  
          const response = await fetch(apiUrl);
          const data = await response.json();
  
          if (data.results && data.results.length > 0) {
            const location = data.results[0];
            this.foundLocation = location;
            console.log('Location:', location);
            // Lakukan sesuatu dengan data lokasi yang ditemukan
          }
        } catch (error) {
          console.error('Error fetching location data:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .location-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #0fc7ff;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .location-widget h2 {
    color: #333;
    font-size: 24px;
    margin-bottom: 20px;
  }
  
  .location-widget p {
    color: #666;
  }
  
  .location-input {
    margin-top: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .location-input label {
    display: block;
    margin-right: 10px;
    color: #333;
    font-size: 16px;
    text-align: right;
    flex: 0 0 80px;
  }
  
  .location-input input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
  }
  
  .location-input button {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .location-input button:hover {
    background-color: #45a049;
  }
  
  .location-input button:disabled {
    background-color: #ccc;
    color: #999;
    cursor: not-allowed;
  }
  
  .location-details {
    margin-top: 20px;
    text-align: left;
  }
  
  .location-details h3 {
    margin-bottom: 10px;
    color: #333;
    font-size: 18px;
  }
  
  .location-details p {
    margin: 5px 0;
    color: #666;
  }
  
  .error-message {
    color: red;
    margin-top: 10px;
  }
  </style>
  