<template>
  <div class="weather">
    <div class="container">

      <div class="card weather-form">
        <input type="text" class="weather-form_input" placeholder="enter city"> 
        <button class="weather-form_btn">Search</button>
      </div>

      <div class="weather-info">
        <div class="weather-info_text">
          <p class="card">Phuket</p>
          <p class="card">29C</p>
          <p class="card">Sunny</p>
        </div>
      </div>
      
    </div>

    <div class="weather-bg">
      <div>
        <img class="weather-bg_img bg" src="./assets/moon.jpg" alt="App Background">
        <img class="weather-bg overcast" src="./assets/overcast.jpg" alt="Overcast">
        <img class="weather-bg partly-cloudy" src="./assets/partly-cloudy.jpg" alt="Partly-cloudy">
        <img class="weather-bg sunny" src="./assets/sunny.jpg" alt="Sunny">
      </div>
    </div>
  </div>
</template>

<script>

</script>