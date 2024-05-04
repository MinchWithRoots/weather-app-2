<template>
  <div class="weather" :class="weatherClass">
    <div class="container">

      <div class="card weather-form">
        <input type="text" class="weather-form_input" v-model="searchQuery" @keyup.enter="weatherSearch" placeholder="Enter city"> 
        <button class="weather-form_btn" @click="weatherSearch">Search</button>
      </div>

      <div class="card weather-load" v-if="loading">Loading...</div>

      <div class="weather-info" v-show="!error && location && temperature !== 0 && description">

        <div class="card" v-if="error">Error</div>

        <div class="weather-info_text">
          <p class="card">{{ location }}</p>
          <p class="card">{{ temperature }}°C</p>
          <p class="card">{{ description }}</p>
        </div>
      </div>
      
    </div>

    <div class="weather-bg">
      <div>
        <img class="weather-bg_img bg" src="./assets/bg.jpg" alt="App Background">
        <img class="weather-bg_img overcast" src="./assets/overcast.jpg" alt="Overcast">
        <img class="weather-bg_img partly-cloudy" src="./assets/partly-cloudy.jpg" alt="Partly-cloudy">
        <img class="weather-bg_img sunny" src="./assets/sunny.jpg" alt="Sunny">
        <!-- snow -->
        <img class="weather-bg_img light-snow" src="./assets/light snow.jpg" alt="light snow">
        <img class="weather-bg_img snow" src="./assets/snow.jpg" alt="snow">
        <img class="weather-bg_img heavy-snow" src="./assets/heavy snow.jpg" alt="heavy snow">
        <img class="weather-bg_img rain-and-snow" src="./assets/rain-and-snow.jpg" alt="rain and snow">
        <!-- rain -->
        <img class="weather-bg_img light-rain" src="./assets/light-rain.jpg" alt="light rain">
        <img class="weather-bg_img moderate-rain" src="./assets/moderate-rain.jpg" alt="moderate rain">
        <img class="weather-bg_img heavy-intensity-rain" src="./assets/heavy-intensity-rain.jpg" alt="heavy intensity rain">
        <img class="weather-bg_img very-heavy-rain" src="./assets/very-heavy-rain.jpg" alt="very heavy rain">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
     location: '',
     temperature: 0,
     description: '',
     searchQuery: '',
     loading: false,
     error: false,
   };
  },
  computed: {
    weatherClass() {
      if (this.description.includes('Sunny')) {
        return 'sunny';
      } else if (this.description.includes('Overcast')) {
       return 'overcast';
      } else if (this.description.includes('Partly cloudy')) {
       return 'partly-cloudy';
      } else if (this.description.includes('Light snow')) {
       return 'light snow';
      } else if (this.description.includes('Snow')) {
       return 'snow';
      } else if (this.description.includes('Heavy Snow')) {
       return 'heavy snow';
      } else if (this.description.includes('Rain and snow')) {
       return 'rain-and-snow';
      } else if (this.description.includes('Light rain')) {
       return 'light-rain';
      } else if (this.description.includes('Moderate rain')) {
       return 'moderate-rain';
      } else if (this.description.includes('Heavy intensity rain')) {
       return 'heavy-intensity-rain';
      } else if (this.description.includes('Very heavy rain')) {
       return 'very-heavy-rain';
      }
      else {
       return '';
     }
   }
 },
  methods: {
    weatherSearch() {
      this.loading = true;
      this.error = false;
      fetch(`https://api.weatherapi.com/v1/current.json?key=69ed7b91ab4b4d4f9f282327242604&q=${this.searchQuery}`)
      .then(response => response.json())
       .then(data => {
         this.loading = false;
         this.location = data.location.name;
         this.temperature = data.current.temp_c;
         this.description = data.current.condition.text;
         this.resetSearchQuery();
       })
      .catch(error => {
        this.loading = false;
        this.error = true;
        console.error(error);
      });
    },
    resetSearchQuery() {
      this.searchQuery = '';
    }
  }
};

</script>