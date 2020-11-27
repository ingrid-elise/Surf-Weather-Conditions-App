<template>
  <div class="weatherInfo">
    <div class="conditions">
      <div id="conditionsCurrently" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles">Currently</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherDataTemp.data[0].temp) }} °C   
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
              {{ degToCompass(weatherData.hours[0].swellDirection.noaa) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirection">
              {{ Math.round(weatherData.hours[0].windDirection.noaa) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[0].windDirection.noaa) }}              
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsThreeHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleThreeHoursAhead">+ 3 hours</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherDataTemp.data[3].temp) }} °C
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
              {{ degToCompass(weatherData.hours[3].swellDirection.noaa) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionThree">
              {{ Math.round(weatherData.hours[3].windDirection.noaa) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[3].windDirection.noaa) }}
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsSixHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleSixHoursAhead">+ 6 hours</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(weatherDataTemp.data[6].temp) }} °C
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
              {{ degToCompass(weatherData.hours[6].swellDirection.noaa) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionSix">
              {{ Math.round(weatherData.hours[6].windDirection.noaa) }} m/sec
              <br />
              {{ degToCompass(weatherData.hours[6].windDirection.noaa) }}
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
  data() {
    return {
      weatherData: {},
      weatherDataTemp: {},
      appid: "86043b7267e3ed491c42805b2e2a2fdc",
      apikey: "1c668929b33949458757d6807fb20968",
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
    getSurfReport() {
      // function for API from StormGlass
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
    getWeatherReport() {
      // function for API for airTemp
      fetch(
        `https://api.weatherbit.io/v2.0/forecast/hourly?&lat=${-33.890842}&lon=${151.27429}&key=${this.apikey}&hours=48`,
      )
        .then(response => response.json())
        .then(data => (this.weatherDataTemp = data));
    },
  },
  mounted() {
    this.getSurfReport(); // makes the api load on page load
    this.getWeatherReport(); // for air temp api
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