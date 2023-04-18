<template>
  <div>
    <h1>Mars Rover Photos</h1>
    <div v-if="loading" class="loader"></div>
    <ul v-else>
      <li v-for="photo in photos" :key="photo.id">
        <img :src="photo.img_src" :alt="photo.camera.full_name" />
        <p>{{ photo.rover.name }} - {{ photo.camera.full_name }}</p>
        <p>{{ photo.earth_date }} - {{ photo.rover.status }}</p>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      photos: [],
      loading: true,
     
    };
  },
  mounted() {
    const apiUrl = 'https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos';
    const apiKey = 'WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n';
    const url = `${apiUrl}?sol=1000&api_key=${apiKey}`;

    fetch(url)
      .then(response => response.json())
      .then(data => {
        this.photos = data.photos.slice(0, 5); // Limit to first 10 photos
        this.loading = false;
      })
      .catch(error => console.error(error));
  }
};
</script>

<style>
.loader {
  border: 16px solid #f3f3f3;
  border-top: 16px solid #3498db;
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
