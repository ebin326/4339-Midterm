<script setup>
import { ref } from 'vue'
import axios from 'axios'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  PointElement,
  CategoryScale,
  LinearScale
} from 'chart.js'
import { Line } from 'vue-chartjs'

ChartJS.register(CategoryScale, LinearScale, LineElement, PointElement)

const form_input = ref({
  location: "",
  start_date: "",
  end_date: ""
})

const weatherData = ref([]);
async function fetch_remote_data() {
  chart_data.value = { labels: [], datasets: [] };
  weatherData.value = [];
  
  try {
    const start = new Date(form_input.value.start_date);
    const end = new Date(form_input.value.end_date);

    const options = {
      method: 'GET',
      url: 'https://weatherapi-com.p.rapidapi.com/history.json',
      headers: {
        'X-RapidAPI-Key': '3bf98fb71fmsh9aea682be12f43fp12cf4fjsn3d72f93416f1',
        'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
      }
    };

    for (let date = start; date <= end; date.setDate(date.getDate() + 1)) {
      const isoDate = date.toISOString().split('T')[0];

      const response = await axios.request({
        ...options,
        params: {
          q: form_input.value.location,
          dt: isoDate,
          lang: 'en'
        }
      });

      const forecastDay = response.data.forecast.forecastday[0];
      if (forecastDay) {
        const maxtempf = response.data.forecast.forecastday[0].day.maxtemp_f; // Get maximum temperature
        console.log(`Maximum temperature for ${isoDate}: ${maxtempf}`);

        weatherData.value.push({ date: isoDate, temperature: maxtempf });
      } else {
        console.error(`No forecast data available for ${isoDate}`);
      }
    }
  } catch (error) {
    console.error('Error fetching weather data:', error);
  }
  draw_chart();
}

const chart_data = ref({
  labels: [],
  datasets: [
    {
      label: "Maximum Temperature (°F)", // Update label to Maximum Temperature
      backgroundColor: "#f87979",
      data: [],
    },
  ],
})

const chart_options = ref({
  responsive: true,
  maintainAspectRatio: true,
  scales: {
    x: {
      title: {
        display: true,
        text: "Date",
      },
    },
    y: {
      title: {
        display: true,
        text: "Maximum Temperature (°F)", // Update y-axis label
      },
    },
  },
})

function draw_chart() {
  const labels = weatherData.value.map(entry => entry.date);
  const temperatures = weatherData.value.map(entry => entry.temperature);

  chart_data.value = {
    labels: labels,
    datasets: [
      {
        label: "Maximum Temperature (°F)",
        backgroundColor: "#f87979",
        data: temperatures,
      },
    ],
  }
}
</script>

<!-- Template for Weather Form -->
<template>
  <div class="form-container">
    <form @submit.prevent="fetch_remote_data">
      <div>
        <h2>Weather Data</h2>
        <p>Please fill in the form and use the submit button to load data.</p>
        <label for="location">Location</label>
        <br />
        <input v-model="form_input.location" type="text" required />
      </div>
      <div>
        <label for="def_dt">Select Start Date</label>
        <br />
        <input type="date" v-model="form_input.start_date" required />
      </div>
      <div>
        <label for="end_date">Select End Date</label>
        <br />
        <input type="date" v-model="form_input.end_date" required />
      </div>
      <br />
      <div>
        <button type="submit">Submit</button>
      </div>
    </form>

    <div class="chart-container">
      <div>
        <Line :data="chart_data" :options="chart_options" v-if="chart_data.labels.length > 0" />
      </div>
    </div>
    <!-- Table to display weather data -->
    <div class="table-container">
      <table v-if="weatherData.length > 0">
        <thead>
          <tr>
            <th>Date</th>
            <th>Temperature (°F)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in weatherData" :key="data.date">
            <td>{{ data.date }}</td>
            <td>{{ data.temperature }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.form-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

form {
  margin-bottom: 20px;
}

input[type="text"],
input[type="date"],
button {
  padding: 8px;
  margin-bottom: 10px;
  width: 100%;
  box-sizing: border-box;
}

button {
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.chart-container {
  margin-top: 20px;
}

.table-container {
  margin-top: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

tr:hover {
  background-color: #f1f1f1;
}
</style>
