<template>
  <div id="app">
    <AsteroidGrid @remove="remove" :asteroids="asteroids" header="Near-Earth Objects" />
  </div>
</template>

<script>
import AsteroidGrid from './components/AsteroidGrid.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    AsteroidGrid
  },
  data() {
      return {
        asteroids: []
      }
  },            
  created: function () {
      this.fetchAsteroids();
  },
  methods: {
      fetchAsteroids: function () {
          var apiKey = 'lkgI9to0hRizfzk4xTAxtNTTFkkA4Mtq7y1yW5me';
          var url = 'https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=' + apiKey;
          axios.get(url)
              .then(res => {                                       
                  this.asteroids = res.data.near_earth_objects.slice(0, 10);
              });
      },
      remove: function (index) {
          this.asteroids.splice(index, 1);            
      },
  }
}
</script>

<style>
  [v-cloak] {
    display: none;
  }
</style>
