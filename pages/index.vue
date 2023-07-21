<template>
  <div class="container">
    <div class="container text-center">
      <h1>This is Weather App</h1>
      <div class="mb-3">
        <label for="" class="form-label"> {{ name }} City</label>
        <select
          class="form-select form-select-lg"
          name=""
          id=""
          v-model="name"
          @change="getUrl(name)"
        >
          <option
            selected
            :value="city.name"
            v-for="(city, index) in city.data.data"
            class="text-center"
          >
            {{ city.name }}
          </option>
        </select>
      </div>
    </div>
    <div v-if="pending" class="container flex justify-content-center box">
      <img src="~/assets/loading.gif" alt="" />
    </div>
    <div class="container text-center" v-else>
      <h1 class="animated-text">{{ weather.weather[0].main }}</h1>
      <h5 class="animated-text">
        {{ weather.name }} : <span>{{ weather.main.temp }} °C</span>
      </h5>
      <div class=" flex justify-content-center">
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
        <img
          src="~/assets/Thunderstorms.gif"
          alt=""
          v-if="weather.weather[0].main == 'Thunderstorm'"
          style="height: 200px; width: 20%;"
        />
      </div>
      <h5 class="animated-text">{{ weather.weather[0].description }}</h5>
      <h5 class="animated-text">Feels Like : {{ weather.main.feels_like }} °C</h5>
      <!-- <h1>Minimum Temperature : {{ weather.main.temp_min }}</h1>
    <h1>Maximum Temperature : {{ weather.main.temp_max }}</h1> -->
      <h5 class="animated-text">Wind Speed : {{ weather.wind.speed }}km/hr</h5>
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
  { headers: { Authorization: "Bearer 5SpnFQK-Jtrds-sziYwEOvM1" } }
);
const { data: weather, pending } = await useFetch(url, { refetch: true });
function getUrl(city) {
  url.value = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=edab429d4f4059d040bd14483316c26d&units=metric`;
}
</script>

<style scoped>
.box {
  margin: 10px;
  align-items: center;
  margin-top: 20px;
}
@keyframes myAnimation {
  0% { opacity: 0; transform: translateY(-20px); }
  100% { opacity: 1; transform: translateY(0); }
}
.animated-text {
  animation: myAnimation 2s ease-in-out forwards;
}
</style>
