<template>
  <div class="container">
    <h2>Weather App</h2>
    <button @click="getWeatherList">Get data</button>
    <div v-for="weatherdata in weatherList" :key="weatherdata.id">
      <p>{{ weatherdata.title }}/p></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "weater",
  data() {
    return {
      weatherList: []
    };
  },
  methods: {
    getWeatherList() {
      //   fetch("https://jsonplaceholder.typicode.com/posts")
      //     .then(response => response.json())
      //     .then(data => (this.weatherList = data));
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then(response => (this.weatherList = response.data));
    }
  }
};
</script>

<style scoped></style>
