<template>
  <div class="container">
    <div class="container text-center">
    <h1>This is Weather App</h1>
    <div class="form-group">
      <label for="my-select">{{ name }} City</label>
      <select id="my-select" class="form-control" name=""
      v-model="name"
      @change="getUrl(name)">
        <option selected
          :value="city.name"
          v-for="(city, index) in city.data.data"
          class="text-center" >
          {{ city.name }}
        </option>
      </select>
    </div>
  </div>
  <div v-if="pending" class="container text-center box">
<img src="~/assets/loading.gif" alt="">
  </div>
  <div class="container text-center" v-else >
 
    <h1>{{ weather.weather[0].main }}</h1>
    <h5>{{ weather.name }} : <span>{{ weather.main.temp }} °C</span></h5>
    <div>
      <img
        src="~/assets/rainy.gif"
        alt=""
        v-if="weather.weather[0].main == 'Rain'"
      />

      <img
        src="~/assets/cloudy.gif"
        alt=""
        v-if="weather.weather[0].main == 'Clouds'"
      />

      <img
        src="~/assets/sun.gif"
        alt=""
        v-if="weather.weather[0].main == 'Clear'"
      />

      <img
        src="~/assets/wind.gif"
        alt=""
        v-if="weather.weather[0].main == 'Wind'"
      />
    </div>
    <h1>{{ weather.weather[0].description }}</h1>
    <h1>Feels Like : {{ weather.main.feels_like }} °C </h1>
    <!-- <h1>Minimum Temperature : {{ weather.main.temp_min }}</h1>
    <h1>Maximum Temperature : {{ weather.main.temp_max }}</h1> -->
    <h1>Wind Speed : {{ weather.wind.speed }}km/hr</h1>

  </div>
  </div>
</template>

<script setup>
let name = ref("Dharan");
const url = ref(
  `https://api.openweathermap.org/data/2.5/weather?q=Dharan&appid=edab429d4f4059d040bd14483316c26d&units=metric`
);
const { data: city } = await useFetch(
  "https://www.nepallocation.com.np/api/v1/city/list",
  { headers: { Authorization: "Bearer 5SpnFQK-Jtrds-sziYwEOvM1" }}
);
const { data: weather,pending } = await useFetch(url, { refetch: true });
function getUrl (city){
  url.value = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=edab429d4f4059d040bd14483316c26d&units=metric`;
};

</script>

<style scoped>
.box{
  margin: 10px;
  align-items: center;
  margin-top: 20px;
}
</style>
