<template>
  <div id="app" class="container">
    <select v-model="section">
      <option v-for="section in sections" :key="section" :value="section">{{ section }}</option>
    </select>
    <hr />
    <button @click="getPosts(section)">Retrieve</button>

    <NewList :results="results" />
  </div>
</template>

<script>
import axios from "axios";
import NewList from "@/components/NewList.vue";
const SECTIONS = "almay, alva, anna sui, annabelle, benefit, boosh";
const NYTBaseUrl =
  "http://makeup-api.herokuapp.com/api/v1/products.json?brand=";
//makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline
function buildUrl(url) {
  return NYTBaseUrl + url;
}

export default {
  name: "App",
  components: {
    NewList
  },
  data() {
    return {
      results: [],
      sections: SECTIONS.split(", "), // create an array of the sections
      section: "maybelline" // set default section to 'home'
    };
  },
  mounted() {
    this.getPosts("this.section");
  },
  methods: {
    getPosts(section) {
      let url = buildUrl(section);
      axios
        .get(url)
        .then(response => {
          this.results = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
</style>
