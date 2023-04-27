<template>
  <div class="space">
    <div v-if="savedImages.length > 0">
      <h2>Saved Images</h2>
      <div class="saved-images">
        <div v-for="(image, index) in savedImages" :key="index" class="saved-image">
          <img :src="image.url" />
          <p>{{ image.title }}</p>
          <p>{{ image.explanation }}</p>
          <button @click="deleteImage(index)">Delete Image</button>
        </div>
      </div>
    </div>
    <h1>Astronomy Picture of the Day</h1>

    <div v-if="image">
      <img :src="image.url" :alt="image.title" />
      <p>{{ image.title }}</p>
      <p>{{ image.explanation }}</p>
      <button @click="downloadImage">Save Image</button>
    </div>
    <div v-else>
      <img src="../assets/loader.gif"/>
    </div>
    <button @click="getNewImage">New Image</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      image: null,
      savedImages: []
    };
  },
  mounted() {
    const savedImages = localStorage.getItem('savedImages');
    if (savedImages) {
      this.savedImages = JSON.parse(savedImages);
    }

    this.getNewImage();
  },
  methods: {
    getNewImage() {
      axios
        .get(
          "https://api.nasa.gov/planetary/apod?api_key=WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n&count=1&thumbs=true"
        )
        .then((response) => {
          const newImage = {
            url: response.data[0].url,
            title: response.data[0].title,
            explanation: response.data[0].explanation
          };
          this.image = newImage;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    downloadImage() {
      this.savedImages.push(this.image);
      localStorage.setItem('savedImages', JSON.stringify(this.savedImages));
    },
    deleteImage(index) {
      this.savedImages.splice(index, 1);
      localStorage.setItem('savedImages', JSON.stringify(this.savedImages));
    }
  }
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

.saved-images {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 24px;
}

.saved-image {
  max-width: 100%;
}

button {
  display: inline-block;
  padding: 12px 24px;
  font-size: 18px;
  font-weight: 600;
  text-transform: uppercase;
  color: #fff;
  background-color: #031660;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #4778b4;
}
</style>
