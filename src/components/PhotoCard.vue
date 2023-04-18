<template>
  <div class="space">
    <h1>Astronomy Picture of the Day</h1>
    <div v-if="image">
      <img :src="image" :alt="title" />
      <p>{{ title }}</p>
      <p>{{ explanation }}</p>
    </div>
    <div v-else>
      <img src="../assets/loader.gif"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      image: "",
      title: "",
      explanation: "",
    };
  },
  mounted() {
    axios
      .get(
        "https://api.nasa.gov/planetary/apod?api_key=WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n&count=1&thumbs=true"
      )
      .then((response) => {
        this.image = response.data[0].url;
        this.title = response.data[0].title;
        this.explanation = response.data[0].explanation;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
div {
  background-color: #0b0c10;
  color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 24px;
  font-family: 'Montserrat', sans-serif;
}

.space img {
  max-width: 100%;
  border-radius: 8px;
  box-shadow: 0 0 16px rgba(255, 255, 255, 0.2);
  margin-bottom: 24px;
}

.space h2 {
  font-size: 36px;
  font-weight: 700;
  text-align: center;
  margin-bottom: 24px;
}

.space p {
  font-size: 18px;
  line-height: 1.5;
  text-align: justify;
  margin-bottom: 24px;
}
</style>