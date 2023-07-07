<template>
    <div class="photo-widget">
      <h2 class="widget-title">{{ title }}</h2>
      <div class="photo-container">
        <img :src="photoUrl" :alt="title" />
      </div>
      <button class="load-button" @click="getRandomPhoto">Muat Foto Baru</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        title: '',
        photoUrl: '',
      };
    },
    mounted() {
      this.getRandomPhoto();
    },
    methods: {
      async getRandomPhoto() {
        try {
          const apiKey = '38037020-2c48722c03be8437a05b588e6';
          const apiUrl = `https://pixabay.com/api/?key=${apiKey}&q=nature&image_type=photo&orientation=horizontal`;
  
          const response = await fetch(apiUrl);
          const data = await response.json();
  
          const randomIndex = Math.floor(Math.random() * data.hits.length);
          const randomPhoto = data.hits[randomIndex];
  
          this.title = randomPhoto.tags;
          this.photoUrl = randomPhoto.webformatURL;
        } catch (error) {
          console.error('Error fetching random photo:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .photo-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .widget-title {
    margin: 0;
    font-size: 24px;
    text-align: center;
    color: #0fc7ff;
  }
  
  .photo-container {
    width: 100%;
    max-width: 500px;
    height: 300px;
    margin-top: 10px;
    overflow: hidden;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  .photo-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }
  
  .load-button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 16px;
    font-weight: bold;
    color: #fff;
    background-color: #0fc7ff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .load-button:hover {
    background-color: #e64a19;
  }
  
  .load-button:focus {
    outline: none;
  }
  
  .load-button:active {
    transform: translateY(1px);
  }
  </style>
  