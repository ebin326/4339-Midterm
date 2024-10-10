<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Chart from 'chart.js/auto';

</script>

<template>
  <header>
    <div class="wrapper">
      <nav class="navbar">
    <div class="navbar-left">
      <ul>
        <router-link to="/">CIS 4339 Midterm</router-link>
      </ul>
    </div>
    <div class="navbar-right">
      <ul>
        <router-link to="/">Home</router-link>
        <router-link to="/form">Form</router-link>
      </ul>
    </div>
  </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  background-color: #3498db; /* Change the background color to a nice blue color */
  padding: 15px 20px; /* Increase the padding to make the navigation bar bigger */
  height: 70px; /* Set a specific height for the navigation bar */
}

nav a {
  color: white;
  text-decoration: none;
  padding: 8px 12px; /* Adjust padding for text */
  margin: 0 10px;
  border-radius: 10px;
  font-weight: bold; /* Make the text bold */
  text-transform: uppercase; /* Convert text to uppercase */
}

nav a:hover {
  background-color: #555;
}
</style>
