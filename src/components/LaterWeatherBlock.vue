<template>
  <div class="weatherInfo">
    <div class="conditions">
      <div id="conditionsCurrently" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles">7 am</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(this.getSevenAmTemp()) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightId">
              {{ this.getSevenWaveHt() }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionId">
              {{ degToCompass(this.getSevenSwellHt()) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirection">
              {{ Math.round(this.getSevenWindDirection()) }} m/sec
              <br />
              {{ degToCompass(this.getSevenWindDirection()) }}
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsThreeHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleThreeHoursAhead">Midday</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(this.getMiddayTemp()) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightThreeAhead">
              {{ this.getMiddayWaveHt() }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionThree">
              {{ degToCompass(this.getMiddaySwellHt()) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionThree">
              {{ Math.round(this.getMiddayWindDirection()) }} m/sec
              <br />
              {{ degToCompass(this.getMiddayWindDirection()) }}
            </p>
          </div>
        </div>
      </div>

      <div id="conditionsSixHoursAhead" class="conditionsCurrentlyClass">
        <div class="conditionsFlex">
          <p class="smallTitles" id="titleSixHoursAhead">6 pm</p>
          <p class="pConditions" id="airTempId">
            {{ Math.round(this.getSixPmTemp()) }} °C
          </p>
          <div class="waveHeightContainer">
            <img
              alt="wave height icon"
              src="../assets/SurfingIconsSVG/wave.png"
              class="wave-height-icon"
            />
            <p class="pConditions" id="waveHeightSixAhead">
              {{ this.getSixPmWaveHt() }} m
            </p>
          </div>
          <div class="swellDirectionContainer">
            <img
              alt="swell direction icon"
              src="../assets/SurfingIconsSVG/compass.png"
              class="swell-direction-icon"
            />
            <p class="pConditions" id="swellDirectionSix">
              {{ degToCompass(this.getMiddaySwellHt()) }}
            </p>
          </div>
          <div class="windDirectionContainer">
            <img
              alt="wind direction icon"
              src="../assets/SurfingIconsSVG/wind.png"
              class="wind-direction-icon"
            />
            <p class="pConditions" id="windSpeedDirectionSix">
              {{ Math.round(this.getSixPmWindDirection()) }} m/sec
              <br />
              {{ degToCompass(this.getSixPmWindDirection()) }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LaterWeatherBlock",
  
  data() {
    return {
      weatherData: {},
      params3: [
        "airTemperature",
        "waveHeight",
        "swellDirection",
        "windSpeed",
        "windDirection"
      ],
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
      return datetime + 86400 + 86400 + 86400 + 86400; // adds 4 days in milisec to current date/time and updates timeframe
    },
    getStartTime() {
      let datetime = Math.round(new Date().getTime() / 1000);
      return datetime + 86400;
    },
    getNewTime() { 
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 2); // getting tomorrow and adding 2 day (need to add 2 as 1 sometimes only showed current day, depending on what time of day it was)
      const tomorrowISO = tomorrow.toISOString(); // converting to ISO string
      const tomorrowHour = tomorrowISO.slice(0, 11); // slicing off time
      const apiFormatTom = tomorrowHour + "07:00:00+00:00"; // adding 7am hours
    //   console.log(apiFormatTom); // 7am time in 2 days time
      return apiFormatTom;
    },
    getMiddayTime() {
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 2);
      const tomorrowISO = tomorrow.toISOString();
      const tomorrowHour = tomorrowISO.slice(0, 11);
      const apiFormatTom = tomorrowHour + "12:00:00+00:00"; // adding to change to search for 12pm
    //   console.log(apiFormatTom);
      return apiFormatTom;
    },
    getSixPmTime(){
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 2);
      const tomorrowISO = tomorrow.toISOString();
      const tomorrowHour = tomorrowISO.slice(0, 11);
      const apiFormatTom = tomorrowHour + "18:00:00+00:00"; // adding to changing to search for 6pm
      return apiFormatTom;
    },
    getSevenAmTemp() {
      let sevenAmTemp = this.getNewTime();
      //console.log(sevenAmTemp) // to clarify v-on:click is working
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sevenAmTemp) {
          return this.weatherData.hours[i].airTemperature.sg; 
        }
      }
    },
    getSevenWaveHt() {
      let sevenAmWaveHt = this.getNewTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sevenAmWaveHt) {
          return this.weatherData.hours[i].waveHeight.sg; 
        }
      }
    },
    getSevenSwellHt() {
      let sevenAmSwellHt = this.getNewTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sevenAmSwellHt) {
          return this.weatherData.hours[i].swellDirection.noaa; 
        }
      }
    }, 
    getSevenWindDirection() {
      let sevenAmWindDirection = this.getNewTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sevenAmWindDirection) {
          return this.weatherData.hours[i].windDirection.noaa; 
        }
      }
    },
    getMiddayTemp(){
      let midday = this.getMiddayTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === midday){
          return this.weatherData.hours[i].airTemperature.sg;
        }
      }
    },
    getMiddayWaveHt(){
      let middayWaveHt = this.getMiddayTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === middayWaveHt) {
          return this.weatherData.hours[i].waveHeight.sg;
        }
      }
    },
    getMiddaySwellHt(){
      let middaySwellHt = this.getMiddayTime(); 
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === middaySwellHt) {
          return this. weatherData.hours[i].swellDirection.noaa;
        }
      }
    },
    getMiddayWindDirection(){
      let middayWindDirection = this.getMiddayTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === middayWindDirection) {
          return this.weatherData.hours[i].windDirection.noaa;
        }
      }
    },
    getSixPmTemp(){
      let sixpm = this.getSixPmTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sixpm){
          return this.weatherData.hours[i].airTemperature.sg;
        }
      }
    },
    getSixPmWaveHt(){
      let sixPmWaveHt = this.getSixPmTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sixPmWaveHt) {
          return this.weatherData.hours[i].waveHeight.sg; 
        }
      }
    },
    getSixPmSwellHt(){
      let sixPmSwellHt = this.getSixPmTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sixPmSwellHt){
          return this.weatherData.hours[i].swellDirection.noaa;
        }
      }
    },
    getSixPmWindDirection(){
      let sixPmWindDirection = this.getSixPmTime();
      for (var i = 0; i < 72; i++) {
        if (this.weatherData.hours[i].time === sixPmWindDirection){
          return this.weatherData.hours[i].windDirection.noaa;
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
          this.params3
        }&start=${this.getStartTime()}&end=${this.getEndTime()}`, // Main weather API
        { headers }
      )
        .then(response => response.json())
        .then(data => (this.weatherData = data));
    },
  },
  mounted() {
    this.getSurfReport(); // makes the api load on page load
  }
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
    background-color: #202C91;
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