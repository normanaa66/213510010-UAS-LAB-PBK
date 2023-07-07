<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">

    <aside class="sidebar">
      <ul class="nav-menu">
        <li class="nav-item"><router-link to="/" class="nav-link">Weather</router-link></li>
        <li class="nav-item"><router-link to="/location" class="nav-link">Location</router-link></li>
        <li class="nav-item"><router-link to="/stopwatch" class="nav-link">Stopwatch</router-link></li>
        <li class="nav-item"><router-link to="/tictactoe" class="nav-link">Tic Tac Toe</router-link></li>
        <li class="nav-item"><router-link to="/photo" class="nav-link">Photo</router-link></li>
      </ul>
    </aside>
    <main class="main-content">
      <router-view></router-view>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  display: flex;
  flex-direction: row;
  height: 100vh;
}

.sidebar {
  background-color: #6eb2ff;
  padding: 20px;
  color: #ffffff;
  min-width: 200px;
}

.nav-menu {
  list-style: none;
  padding: 0;
  margin: 0;
}

.nav-item {
  margin-bottom: 10px;
}

.nav-link {
  position: relative;
  padding: 5px 10px;
  display: block;
  font-family: 'Poppins', sans-serif;
  font-size: 18px;
  transition: color 0.3s ease;
}

.nav-link::before {
  content: '';
  position: absolute;
  width: 3px;
  height: 100%;
  background-color: #ffffff;
  left: 0;
  top: 0;
  transform: scaleY(0);
  transform-origin: top;
  transition: transform 0.3s ease;
}

.nav-link:hover::before {
  transform: scaleY(1);
}

.main-content {
  flex-grow: 1;
  padding: 20px;
}

/* Animasi Fade In */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Animasi Slide In */
@keyframes slideIn {
  from {
    transform: translateY(-20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

/* Animasi Scale In */
@keyframes scaleIn {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

/* Animasi Rotate In */
@keyframes rotateIn {
  from {
    transform: rotate(-90deg);
    opacity: 0;
  }
  to {
    transform: rotate(0deg);
    opacity: 1;
  }
}

/* Menggunakan animasi pada elemen */
.sidebar {
  animation: slideIn 0.5s ease;
}

.nav-link {
  animation: fadeIn 0.3s ease;
}

.main-content {
  animation: rotateIn 0.5s ease;
}

</style>
