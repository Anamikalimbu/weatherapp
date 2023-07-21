<template>
    <div>
        <div class="flex justify-center">
      <label for="" class="text-white lg:text-3xl md:text:xl"
        >Search City</label
      >
      <input
        type="text"
        v-model="name"
        class="border py-2 px-2 mx-2 bg-white text-black"
        placeholder="Search City"
      />
      <button
        @click="getUrl(name)"
        class="py-2 px-5 bg-blue-500 text-white rounded-full"
      >
        <i class="fa-solid fa-magnifying-glass"></i>
      </button>
    </div>
    <div v-if="pending" class="container flex justify-content-center box">
      <img src="~/assets/loading.gif" alt="" />
    </div>
    <div class=" text-center mt-20 transform -translate-y-10 hover:-translate-y-4 transition duration-700 grid grid-cols-4" v-else>
      <div class=" col-span-4   border border-white bg-slate">
        <h1 class="pt-2">{{ weather.weather[0].main }}</h1>
      <h5>
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
      <h5>{{ weather.weather[0].description }}</h5>
      <h5>Feels Like : {{ weather.main.feels_like }} °C</h5>
      <!-- <h1>Minimum Temperature : {{ weather.main.temp_min }}</h1>
    <h1>Maximum Temperature : {{ weather.main.temp_max }}</h1> -->
      <h5 class="pb-2">Wind Speed : {{ weather.wind.speed }}km/hr</h5>
      </div>
    </div>
    </div>
</template>

<script setup>
let name = ref("Dharan");
const url = ref(
  `https://api.openweathermap.org/data/2.5/weather?q=Dharan&appid=edab429d4f4059d040bd14483316c26d&units=metric`
);
const { data: city } = await useFetch(
  "https://www.nepallocation.com.np/api/v1/city?name=Dharan",
  { headers: { Authorization: "Bearer 5SpnFQK-Jtrds-sziYwEOvM1" } }
);
const { data: weather,pending } = await useFetch(url, { refetch: true });
// function getUrl(city) {
//     url.value = `https://www.themealdb.com/api/json/v1/1/search.php?s=${city}`;
// }
function getUrl(city) {
  url.value = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=edab429d4f4059d040bd14483316c26d&units=metric`;
}
</script>

<style  scoped>
.box {
  margin: 10px;
  align-items: center;
  margin-top: 20px;
}
</style>