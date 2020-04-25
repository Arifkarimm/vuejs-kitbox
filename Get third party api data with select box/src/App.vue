<template>
  <div class="container" id="app">
    <h3 class="text-center">VueNews</h3>

    <section class="callout secondary">
      <h5 class="text-center">Filter by Category</h5>
      <form>
        <div class="row">
          <div class="large-6 columns">
            <select v-model="section">
              <option v-for="section in sections" :value="section" :key="section">{{ section }}</option>
            </select>
          </div>
          <div class="medium-6 columns">
            <a @click="getPosts(section)" class="button expanded">Retrieve</a>
          </div>
        </div>
      </form>
    </section>

    <h5 class="text-center uppercase" v-if="!loading">
      <strong>{{ title }}</strong>
    </h5>
    <div v-if="loading" class="loader">
      <img
        src="http://cdnjs.cloudflare.com/ajax/libs/semantic-ui/0.16.1/images/loader-large.gif"
        alt="loader"
      />
    </div>

    <NewList v-if="!loading" :results="results"></NewList>
  </div>
</template>

<script>
import axios from "axios";
import NewList from "@/components/NewList.vue";
const NYTBaseUrl = "https://api.nytimes.com/svc/topstories/v2/";
const ApiKey = "M9TrAt5S55PzNeUR9HQetS6v6GkQF4yT";
const SECTIONS =
  "home, arts, automobiles, books, business, fashion, food, health, insider, magazine, movies, national, nyregion, obituaries, opinion, politics, realestate, science, sports, sundayreview, technology, theater, tmagazine, travel, upshot, world"; // From NYTimes

function buildUrl(url) {
  return NYTBaseUrl + url + ".json?api-key=" + ApiKey;
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
      section: "home", // set default section to 'home'
      loading: true,
      title: ""
    };
  },
  mounted() {
    this.getPosts("home");
  },
  methods: {
    getPosts(section) {
      let url = buildUrl(section);
      axios
        .get(url)
        .then(response => {
          this.loading = false;
          this.results = response.data.results;
          let title =
            this.section !== "home"
              ? "Top stories in '" + this.section + "' today"
              : "Top stories today";
          this.title = title + "(" + response.data.num_results + ")";
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
.container {
  padding: 20px 0;
}
.column:last-child:not(:first-child),
.columns:last-child:not(:first-child) {
  float: left;
}
.main_heading {
  margin: 10px 0 30px;
}
.callout {
  margin-bottom: 40px;
}
select {
  text-transform: capitalize;
}
.loader {
  text-align: center;
  padding: 40px;
}
.uppercase {
  text-transform: uppercase;
}
</style>
