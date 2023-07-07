<template>
    <div class="stopwatch-widget">
      <h2>Stopwatch</h2>
      <div class="stopwatch-display">
        <p>{{ formatTime }}</p>
      </div>
      <div class="stopwatch-controls">
        <button @click="startStopwatch" :disabled="isRunning">Start</button>
        <button @click="stopStopwatch" :disabled="!isRunning">Stop</button>
        <button @click="resetStopwatch">Reset</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isRunning: false,
        startTime: null,
        elapsedTime: 0,
      };
    },
    computed: {
      formatTime() {
        const milliseconds = this.elapsedTime % 1000;
        const seconds = Math.floor(this.elapsedTime / 1000) % 60;
        const minutes = Math.floor(this.elapsedTime / 60000) % 60;
        const hours = Math.floor(this.elapsedTime / 3600000);
  
        return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${milliseconds.toString().padStart(3, '0')}`;
      },
    },
    methods: {
      startStopwatch() {
        if (!this.isRunning) {
          this.isRunning = true;
          this.startTime = Date.now();
  
          this.timerInterval = setInterval(() => {
            this.elapsedTime = Date.now() - this.startTime;
          }, 10);
        }
      },
      stopStopwatch() {
        if (this.isRunning) {
          this.isRunning = false;
          clearInterval(this.timerInterval);
        }
      },
      resetStopwatch() {
        this.isRunning = false;
        clearInterval(this.timerInterval);
        this.elapsedTime = 0;
      },
    },
  };
  </script>
  
  <style scoped>
  .stopwatch-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    background-color: #0fc7ff;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .stopwatch-widget h2 {
    color: #333;
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .stopwatch-display {
    background-color: #333;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
  }
  
  .stopwatch-display p {
    color: #fff;
    font-size: 40px;
    margin: 0;
  }
  
  .stopwatch-controls {
    text-align: center;
  }
  
  .stopwatch-controls button {
    padding: 10px 20px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin: 5px;
  }
  
  .stopwatch-controls button:hover {
    background-color: #45a049;
  }
  
  .stopwatch-controls button:disabled {
    background-color: #ccc;
    color: #999;
    cursor: not-allowed;
  }
  </style>
  