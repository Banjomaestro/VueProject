<template>

    <div>
      <input type="text" v-model="search" placeholder="Chercher un chien">
      <label for="asteroid-sort">Trier par : </label>
      <select v-model="asteroidsSortType" id="asteroid-sort">
        <option value="AZName">Name from A à Z</option>
        <option value="ZAName">Name from Z à A</option>
      </select>
      <h2>Asteroids Near Earth</h2>
      <ul>
        <li v-for="asteroid in asteroids" :key="asteroid.neo_reference_id">
          <strong>{{ asteroid.name }}</strong>
          <br>
          Closest approach date: {{ asteroid.close_approach_data[0].close_approach_date_full }}
          <br>
          Miss distance: {{ asteroid.close_approach_data[0].miss_distance.kilometers }} km
          <br>
          Min diameter: {{ asteroid.estimated_diameter.meters.estimated_diameter_min }} m
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {

    computed:{
      
    },
    data() {
      return {
        asteroids: [],
        search: "",
        asteroidsSortType:"AZName"
      }
    },
    mounted() {
      fetch("https://api.nasa.gov/neo/rest/v1/feed?start_date=2000-01-01&end_date=2000-01-08&api_key=WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n")
        .then(response => response.json())
        .then(data => {
          const asteroidList = Object.values(data.near_earth_objects).flat();
          this.asteroids = asteroidList.sort((a, b) => {
            return a.close_approach_data[0].miss_distance.kilometers - b.close_approach_data[0].miss_distance.kilometers;
          });
        }).then(data => {
          const asteroidList = Object.values(data.near_earth_objects).flat();
          this.asteroids = asteroidList.sort((a, b) => {
            return a.estimated_diameter.meters.estimated_diameter_min - b.estimated_diameter.meters.estimated_diameter_min;
          });
        });
    }
  }
  </script>
  
  <style>
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  li {
    background-color: #000000;
    border-radius: 10px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.2);
    margin-bottom: 20px;
    padding: 2rem;
    position: relative;
  }
  li:before {
    content: '';
    display: block;
    width: 0;
    height: 0;
    position: absolute;
    top: 0;
    left: 0;
    border-top: 20px solid #ffaf49;
    border-left: 20px solid transparent;
    z-index: 1;
  }
  li:after {
    content: '';
    display: block;
    width: 0;
    height: 0;
    position: absolute;
    bottom: 0;
    right: 0;
    border-bottom: 20px solid #ffaf49;
    border-right: 20px solid transparent;
    z-index: 1;
  }
  li strong {
    font-weight: bold;
    font-size: 1.2em;
    color: #ffaf49;
  }
  li span {
    display: block;
    font-size: 0.8em;
    color: #666;
    margin-top: 10px;
  }
  li:hover {
    transform: translateY(-5px);
    transition: transform 0.3s ease-in-out;
  }

  .input{

  }
</style>
