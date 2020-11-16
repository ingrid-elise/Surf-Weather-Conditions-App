<template>
  <div class="home">
    <CurrentDate />
    <div id="weatherIcon">
      <img id="sun-icon" alt="sun-icon" src="../assets/sunny.svg" />
    </div>
    <HelloWorld msg="Hello, Bondi Beach" />
    <div id="todayFutureTitles">
      <!-- Titles for today,tomorrow,after -->
      <button
        class="smallTitles"
        id="currentlyTitle"
        v-on:click="component = 'today'"
      >
        <!-- <p
        v-on:click="changeTimeframe(0);"
        v-bind:class="{ active: timeframe === 0 }"
      > -->
        Today
      </button>
      <!-- <p
        v-on:click="changeTimeframe(1); getSevenAm()"
        v-bind:class="{ active: timeframe === 1 }"
      > -->
      <button
        class="smallTitles"
        id="tomorrowTitle"
        v-on:click="component = 'tomorrow'"
      >
        Tomorrow
      </button>
      <button
        class="smallTitles"
        id="afterTitle"
        v-on:click="component = 'after'"
      >
        After
      </button>
    </div>
    <component :is="component"></component>
    <AdditionalInfo />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import CurrentDate from "@/components/CurrentDate.vue";
import WeatherDataBlocks from "@/components/WeatherDataBlocks.vue";
import TomorrowWeatherBlock from "@/components/TomorrowWeatherBlock.vue";
import AfterWeatherBlock from "@/components/AfterWeatherBlock";
import AdditionalInfo from "@/components/AdditionalInfo.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
    CurrentDate,
    'today': WeatherDataBlocks,
    'tomorrow': TomorrowWeatherBlock,
    'after': AfterWeatherBlock,
    AdditionalInfo
  },
  data() {
    return {
      component: 'today',
      
       // this shows which component is the default one showing
      // params: [
      //   "cloudCover",
      //   "airTemperature",
      //   "waveHeight",
      //   "swellDirection",
      //   "windSpeed",
      //   "windDirection",
      // ],
      // weatherData: {}, // empty object or array, doesn't matter.
      // timeframe: 0, // default timeframe showing timeframe of currently (time now)
    };
  },
  methods: {
    // changeTimeframe(num) {
    //   console.log(num);      // number changes depending on which title is clicked
    //   this.timeframe = num;
    //   this.getSurfReport(); // updates the api data after we get new values for time from getEndTime()/getStartTime()
    // },
    // getEndTime() {
    //   let datetime = Math.round(new Date().getTime() / 1000); // gets new date/time
    //   return datetime + 86400 + 86400 + 86400; // adds 3 days in milisec to current date/time and updates timeframe
    // },
    // getStartTime() {
    //   let datetime = Math.round(new Date().getTime() / 1000);
    //   return datetime + 86400;
    // },
    // getNewTime() {
    //   const today = new Date();
    //   const tomorrow = new Date(today);
    //   tomorrow.setDate(tomorrow.getDate() + 1); // getting tomorrow and adding 1 day (need to add 2 as 1 sometimes only showed current day, depending on what time of day it was)
    //   const tomorrowISO = tomorrow.toISOString(); // converting to ISO string
    //   const tomorrowHour = tomorrowISO.slice(0, 11); // slicing off time
    //   const apiFormatTom = tomorrowHour + "07:00:00+00:00"; // adding 7am hours
    //   console.log(apiFormatTom); // next 7am time
    //   return apiFormatTom;
    // },
    // getSevenAm() {
    //   let sevenAm = this.getNewTime();
    //   console.log(sevenAm) // to clarify v-on:click is working
    //   for (var i = 0; i < 48; i++) {
    //     if (this.weatherData.hours[i].time === sevenAm) {
    //       console.log(Math.round(this.weatherData.hours[i].airTemperature.sg))
    //       console.log(this.weatherData.hours[i].waveHeight.sg)
    //       console.log("seven am data showing"); // to clarify next 7am data point is showing
    //       return this.weatherData.hours[i].airTemperature.sg;
    //     }
    //   }
    // },
    // getSurfReport() {
    //   // function for API
    //   const headers = {
    //     Authorization:
    //       "411512a6-b996-11ea-9409-0242ac130002-41151364-b996-11ea-9409-0242ac130002"
    //   };
    //   fetch(
    //     `https://api.stormglass.io/v2/weather/point?lat=${-33.890842}&lng=${151.274292}&params=${
    //       this.params
    //     }&start=${this.getStartTime()}&end=${this.getEndTime()}`, // Main weather API
    //     { headers }
    //   )
    //     .then(response => response.json())
    //     .then(data => (this.weatherData = data));
    // },
    // degToCompass(num) {
    //   var val = Math.floor(num / 22.5 + 0.5);
    //   var arr = [
    //     "N",
    //     "NNE",
    //     "NE",
    //     "ENE",
    //     "E",
    //     "ESE",
    //     "SE",
    //     "SSE",
    //     "S",
    //     "SSW",
    //     "SW",
    //     "WSW",
    //     "W",
    //     "WNW",
    //     "NW",
    //     "NNW"
    //   ];
    //   return arr[val % 16];
    // }
  }
  // mounted() {
  //   this.getSurfReport(); // makes the api load on page load
  // }
};
</script>

<style scoped>
button {
  border: none;
  background-color: #ffb45c;
  border-radius: 5px;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;
  color: #2c3e50;
  font-weight: bold;
}
#sun-icon {
  display: flex;
  max-width: 100px;
  height: auto;
  margin: auto;
  padding: 20px;
}
body,
html {
  width: 100%;
  margin: 0px;
  padding: 0px;
  background-color: #f7f7f7;
  font-family: "Montserrat", sans-serif;
}
.smallTitles {
  margin-bottom: 10px;
  margin-top: 10px;
}
#todayFutureTitles {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin-right: 20px;
}
</style>
