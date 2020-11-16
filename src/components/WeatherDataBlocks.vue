<template>
  <div class="weatherInfo">
    <div class="conditions">
      <div id="conditionsCurrently" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles">Currently</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherData.hours[0].airTemperature.sg) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightId">
              {{ weatherData.hours[0].waveHeight.sg }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionId">
              {{ degToCompass(weatherData.hours[0].swellDirection.sg) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirection">
              {{ Math.round(weatherData.hours[0].windDirection.sg) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[0].windDirection.sg) }}
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsThreeHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleThreeHoursAhead">+ 3 hours</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherData.hours[3].airTemperature.sg) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightThreeAhead">
              {{ weatherData.hours[3].waveHeight.sg }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionThree">
              {{ degToCompass(weatherData.hours[3].swellDirection.sg) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionThree">
              {{ Math.round(weatherData.hours[3].windDirection.sg) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[3].windDirection.sg) }}
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsSixHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleSixHoursAhead">+ 6 hours</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherData.hours[6].airTemperature.sg) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightSixAhead">
              {{ weatherData.hours[6].waveHeight.sg }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionSix">
              {{ degToCompass(weatherData.hours[6].swellDirection.sg) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionSix">
              {{ Math.round(weatherData.hours[6].windDirection.sg) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[6].windDirection.sg) }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WeatherDataBlocks",
//   props: ["weatherData"], // passes the weather data UP to the parent (Home)
  data() {
    return {
      weatherData: {},
      params: [
        "airTemperature",
        "waveHeight",
        "swellDirection",
        "windSpeed",
        "windDirection"
      ]
    };
  },
  methods: {
    degToCompass(num) {
      var val = Math.floor(num / 22.5 + 0.5);
      var arr = [
        "N",
        "NNE",
        "NE",
        "ENE",
        "E",
        "ESE",
        "SE",
        "SSE",
        "S",
        "SSW",
        "SW",
        "WSW",
        "W",
        "WNW",
        "NW",
        "NNW"
      ];
      return arr[val % 16];
    },
    getEndTime() {
      let datetime = Math.round(new Date().getTime() / 1000); // gets new date/time
      return datetime + 86400 + 86400 + 86400; // adds 3 days in milisec to current date/time and updates timeframe
    },
    getStartTime() {
      let datetime = Math.round(new Date().getTime() / 1000);
      return datetime + 86400;
    },
    getNewTime() {
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 1); // getting tomorrow and adding 1 day (need to add 2 as 1 sometimes only showed current day, depending on what time of day it was)
      const tomorrowISO = tomorrow.toISOString(); // converting to ISO string
      const tomorrowHour = tomorrowISO.slice(0, 11); // slicing off time
      const apiFormatTom = tomorrowHour + "07:00:00+00:00"; // adding 7am hours
      console.log(apiFormatTom); // next 7am time
      return apiFormatTom;
    },
    getSevenAm() {
      let sevenAm = this.getNewTime();
      console.log(sevenAm) // to clarify v-on:click is working
      for (var i = 0; i < 48; i++) {
        if (this.weatherData.hours[i].time === sevenAm) {
          console.log(Math.round(this.weatherData.hours[i].airTemperature.sg))
          console.log(this.weatherData.hours[i].waveHeight.sg)
          console.log("seven am data showing"); // to clarify next 7am data point is showing
          return this.weatherData.hours[i].airTemperature.sg;
        }
      }
    },
    getSurfReport() {
      // function for API
      const headers = {
        Authorization:
          "411512a6-b996-11ea-9409-0242ac130002-41151364-b996-11ea-9409-0242ac130002"
      };
      fetch(
        `https://api.stormglass.io/v2/weather/point?lat=${-33.890842}&lng=${151.274292}&params=${
          this.params
        }&start=${this.getStartTime()}&end=${this.getEndTime()}`, // Main weather API
        { headers }
      )
        .then(response => response.json())
        .then(data => (this.weatherData = data));
    },
  },
  mounted() {
    this.getSurfReport(); // makes the api load on page load
  },
};
</script>

<style scoped>
.activeColor {
  background-color: burlywood;
}

.waveHeightContainer,
.swellDirectionContainer,
.windDirectionContainer {
  display: flex;
  flex-direction: row;
}

.conditions {
  display: flex;
  flex-direction: row;
  color: #fffffb;
  position: relative;
  margin-top: 20px;
  justify-content: space-around;
  align-items: center;
  width: 100%;
}

#conditionsCurrently {
  display: block;
}

.conditionsCurrentlyClass{
    background-color: #206491;
}

.conditionsFlex {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border-radius: 5px;
  padding-top: 10px;
  width: 30vw;
  height: 60vh;
  color: #fffffb;
}

.pConditions {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3px;
  width: 10vw;
}

#airTempId {
  color: #ffb45c;
}

.smallTitles {
  font-weight: bold;
}

#waveHeightContainer {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.wave-height-icon,
.swell-direction-icon,
.wind-direction-icon {
  display: flex;
  width: auto;
  height: 30px;
  align-items: center;
  justify-content: center;
  padding: 5px;
}

.swell-direction-icon {
  margin-top: 10px;
}

.wind-direction-icon {
  margin-top: 30px;
}
</style>