<template>

    <div>
      <label for="asteroid-sort">Sort by : </label>
      <select v-model="asteroidsSortType" id="asteroid-sort">
        <option value="AZName">Name from A à Z</option>
        <option value="ZAName">Name from Z à A</option>
        <option value="MissDistance">Miss Distance</option>
        <option value="Diameter">Diameter</option>

      </select>
      <div v-if="asteroids">
        <h2>Asteroids which approached Earth today</h2>
        <ul>
          <li v-for="asteroid in asteroidsOrganizedData" :key="asteroid.neo_reference_id">
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
      <div v-else>
      <img src="../assets/loader.gif"/>
    </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "AsteroidsTable",
    computed:{

      asteroidsOrganizedData: function() {
    let sortedAsteroids = [...this.asteroids];
    if (this.asteroidsSortType === "AZName") {
      sortedAsteroids.sort((a, b) => a.name.localeCompare(b.name));
    } else if (this.asteroidsSortType === "ZAName") {
      sortedAsteroids.sort((a, b) => b.name.localeCompare(a.name));
    }else if (this.asteroidsSortType === "MissDistance") {
      sortedAsteroids.sort((a, b) => a.close_approach_data[0].miss_distance.kilometers.localeCompare(b.close_approach_data[0].miss_distance.kilometers));
    }else if (this.asteroidsSortType === "Diameter") {
      sortedAsteroids.sort((a, b) => a.estimated_diameter.meters.estimated_diameter_min - b.estimated_diameter.meters.estimated_diameter_min);
    }
    return sortedAsteroids;
  }
},
    data() {
      return {
        currentDate() {
        const today = new Date();
        return today.toDateString();
      },
      yesterdayDate() {
        const yesterday = new Date();
        yesterday.setDate(yesterday.getDate() - 1);
        return yesterday.toDateString();
      },
        asteroids: [],
        search: "",
        asteroidsSortType:"AZName"
      }
    },
    mounted() {
      const today = new Date().toISOString().slice(0, 10);

    // Subtract one day from today's date to get yesterday's date
    const yesterday = new Date(new Date().getTime() - 24 * 60 * 60 * 1000)
      .toISOString()
      .slice(0, 10);

    const apiUrl = `https://api.nasa.gov/neo/rest/v1/feed?start_date=${yesterday}&end_date=${today}&api_key=WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n`;

    fetch(apiUrl).then(response => response.json())
        .then(data => {
          const asteroidList = Object.values(data.near_earth_objects).flat();
          this.asteroids = asteroidList.sort((a, b) => {
            return a.close_approach_data[0].miss_distance.kilometers - b.close_approach_data[0].miss_distance.kilometers;
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


  /* Outer container for the input field */
.space-input-container {
  position: relative;
  width: 300px;
  height: 50px;
  border-radius: 25px;
  background-color: #959494;
  box-shadow: 0px 0px 10px 0px rgba(255,255,255,0.2);
  overflow: hidden;
  font-family: 'Montserrat', sans-serif;

}

/* Inner container for the label and input */
.space-input-inner {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
}

/* Label for the input */
.space-input-label {
  flex: 1;
  color: #fff;
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Input field */
.space-input {
  flex: 2;
  width: 100%;
  height: 100%;
  padding: 0 20px;
  border: none;
  outline: none;
  background-color: transparent;
  color: #fff;
  font-size: 20px;
  font-weight: bold;
  letter-spacing: 1px;
}

/* Icon to the right of the input */
.space-input-icon {
  flex: 1;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Style the icon */
.space-input-icon i {
  font-size: 24px;
  color: #fff;
  transition: transform 0.3s ease;
}

/* On hover, rotate the icon */
.space-input-icon:hover i {
  transform: rotate(90deg);
}

</style>
