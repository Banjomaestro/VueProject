<template>
  <div id="app">

    <SpaceNavBar/>
    <PhotoCard/>
    <PhotoCard/>

    <button @click="sortAsteroids()">Sort by Distance</button>

    <AsteroidsTable/>
    <FooterComp/>
  </div>
</template>

<script>
import axios from "axios";
import SpaceNavBar from "./components/SpaceNavBar.vue";
import AsteroidsTable from "./components/AsteroidsTable.vue"
import PhotoCard from "./components/PhotoCard.vue"
import FooterComp from "./components/FooterComp.vue"

export default {
    data() {
        return {
            asteroids: [],
        };
    },
    mounted() {
        axios
            .get("https://api.nasa.gov/neo/rest/v1/feed?start_date=2020-03-28&end_date=2023-03-29&api_key=WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n")
            .then((response) => {
            this.asteroids = response.data.near_earth_objects["2023"];
        })
            .catch((error) => {
            console.log(error);
        });
    },
    methods: {
    onClick(asteroid) {
      asteroid.selected = !asteroid.selected;
    },
    sortAsteroids() {
      this.asteroids.sort((a, b) => {
        return a.close_approach_data[0].miss_distance.kilometers -
          b.close_approach_data[0].miss_distance.kilometers;
      });
    },
  },
    components: { SpaceNavBar, AsteroidsTable, PhotoCard, FooterComp }
};
</script>

<style>
  #app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  .footer {
    margin-top: auto;
  }
</style>
