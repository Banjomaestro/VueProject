<template>
  <div>
    <h1>Coronal Mass Ejections</h1>
    <ul>
      <li v-for="cme in cmes" :key="cme.activityID">
        {{ cme.activityID }} - {{ cme.note }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cmes: [],
      apiKey: 'WPtOXNXgwu35UIhBUg8sgxmVlneZKDYL5UAYgc3n',
      
    };
  },
  created() {
    this.fetchCmes();
  },
  methods: {
    
    fetchCmes() {
      const today = new Date().toLocaleDateString();
      
      axios.get(`https://api.nasa.gov/DONKI/CME?startDate=${today}&endDate=${today}&api_key=${this.apiKey}`)
        .then(response => {
          this.cmes = response.data.slice(0,5);
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>
