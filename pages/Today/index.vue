<template>
  <div>
    <div class="grid lg:grid-cols-3 md:grid-cols-1">
      <label for="" class="text-black lg:text-3xl md:text:xl"
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
    <div class=" text-center  mt-20 transform -translate-y-10 hover:-translate-y-4 transition duration-700 grid grid-cols-4" v-else>
      <div class=" col-span-4   border border-white bg-slate">
        <div class=" flex justify-content-center" v-for="(current,index) in weather.current.condition" :key="index">
        <h3>{{ current.text }}</h3>

        <img
          src="~/assets/rainy.gif"
          alt=""
          v-if="current.text == 'Light rain shower'"
        />

        <img
          src="~/assets/cloudy.gif"
          alt=""
          v-if="current.text == 'Partly cloudy'"
        />

        <img
          src="~/assets/sun.gif"
          alt=""
          v-if="current.text == 'Clear'"
        />

        <img
          src="~/assets/wind.gif"
          alt=""
          v-if="current.text == 'Wind'"
        />
        <img
          src="~/assets/Thunderstorms.gif"
          alt=""
          v-if="current.text == 'Thunderstorm'"
          style="height: 200px; width: 20%;"
        />
        
      </div>
      <h5>
        {{ weather.location.name }} : <span>{{ weather.current.temp_c }} °C</span>
      </h5>
      <h5>Date/Time : {{ weather.location.localtime }}</h5>
      <h4> Country : {{ weather.location.country }}</h4>
      <h4>Wind Speed : {{ weather.current.wind_kph }} km/hr</h4>
    
      <!-- <h5>{{ weather.weather[0].description }}</h5>
      <h5>Feels Like : {{ weather.main.feels_like }} °C</h5> -->
      <!-- <h1>Minimum Temperature : {{ weather.main.temp_min }}</h1>
    <h1>Maximum Temperature : {{ weather.main.temp_max }}</h1> -->
      <!-- <h5 class="pb-2">Wind Speed : {{ weather.wind.speed }}km/hr</h5> -->
      </div>
    </div>
  </div>
</template>

<script setup>
let name = ref("Dharan");
const url = ref(
  `https://api.weatherapi.com/v1/current.json?key=8c0c6b6b9fab413481440653232107&q=Dharan&aqi=yes`
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
  url.value = `https://api.weatherapi.com/v1/current.json?key=8c0c6b6b9fab413481440653232107&q=${city}&aqi=yes
`;
}
</script>

<style scoped>
.box {
  margin: 10px;
  align-items: center;
  margin-top: 20px;
}
</style>
