<template>
  <v-card class="weather">
    <div style="display: flex">
      <v-card
        max-width="500"
        height="200"
        style="margin: 2% 2% 2% 7%; padding: 3%"
        elevation="2"
      >
        <v-combobox
          v-model="value"
          :items="cities"
          dense
          label="Select City"
        ></v-combobox>

        <v-btn @click="LogCity()" depressed color="primary"> Search </v-btn>
      </v-card>

      <v-card
        v-if="weather_response"
        width="450"
        height="200"
        style="margin: 2% 2% 2% 7%; padding: 3%"
        elevation="2"
      >
        <div class="data">
          <h3>Temperature : {{ weather_response.main.temp }} *C</h3>
          <h3>Humidity : {{ weather_response.main.humidity }} %</h3>
          <h3>Pressure : {{ weather_response.main.pressure }} hPa</h3>
          <h3>Wind Speed : {{ weather_response.wind.speed }} m/s</h3>
        </div>
      </v-card>

      <v-card
        v-if="weather_response"
        width="200"
        class="rounded-card"
        height="200"
        style="margin: 2% 2% 2% 7%; padding: 3%"
        elevation="2"
      >
        <div
          class="img-container"
          style="display: flex; align-content: center; justify-content: center"
        >
          <img
            style="align-content: center; justify-content: center"
            :src="iconUrl"
            alt="http://openweathermap.org/img/wn/10d@2x.png"
            srcset=""
          />
        </div>
      </v-card>
    </div>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  name: "Weather",
  data() {
    return {
      cities: [
        "Vellore",
        "Chennai",
        "Bangalore",
        "Mumbai",
        "Vijayawada",
        "Vijayapuri",
        "Vijāpur",
        "Vidisha",
        "Vettavalam",
        "Vettaikkaranpudur",
        "Vetapālem",
        "Verna",
        "Verāval",
        "Vepagunta",
        "Venkatagiri",
        "Vengurla",
        "Vemalwāda",
        "Velur",
        "Vellore",
        "Vejalpur",
        "Vedasandūr",
        "Vedaraniyam",
        "Vayalār",
        "Vattalkundu",
        "Vāsudevanallūr",
        "Vasind",
        "Vasco da Gama",
      ],
      iconUrl: "",
      value: null,
      weather_response: null,
    };
  },  
  methods: {
    LogCity() {
      let city = this.value;
      var key = "INSERT KEY HERE";
      var url =
        "https://api.openweathermap.org/data/2.5/weather?q=" +
        city +
        "&units=metric&appid=" +
        key;

      axios.get(url).then((response) => {
        console.log(response.data);
        this.weather_response = response.data;
        this.iconUrl =
          "http://openweathermap.org/img/wn/" +
          response.data.weather[0].icon +
          "@2x.png";
      });
    },
  },
};
</script>

<style scoped>
.rounded-card {
  border-radius: 40%;
}

.v-card {
  background: rgb(255, 255, 255);
}

.weather{
  background: #5996d4 !important ;
  margin: 40px;
}
.v-btn{
  margin-top: 15px;
}
</style>

alpha\vue.config.js

module.exports = {
  devServer: {
    host: 'localhost',
  },
  transpileDependencies: [
    'vuetify'
  ]
}