<template>
<div>
  <div id="furtherInfoSection">
    <h1 id="furtherCondTitle">Further Conditions</h1>
    <div id="blockOfConditions">
      <p class="pConditions" id="sunRise">
        Sunrise <br />{{ dateFormat(new Date(sunMoonData.data[0].sunrise)) }}
      </p>
      <p class="pConditions" id="sunSet">
        Sunset <br />{{ dateFormat(new Date(sunMoonData.data[0].sunset)) }}
      </p>
      <p class="pConditions" id="tideMoon">
        Tide <br />
        {{ tideData.data[0].type }} at
        {{ dateFormat(new Date(tideData.data[0].time)) }}
      </p>
      <p class="pConditions" id="wavePeriodId">
        Wave period <br />{{ Math.round(weatherData.hours[0].wavePeriod.sg) }}
      </p>
      <p class="pConditions" id="moonInput">
        Moon <br />
        {{ sunMoonData.data[0].moonPhase.current.text }}
      </p>
      <p class="pConditions" id="uvIndexInput">
        UV Index <br />{{ Math.round(uvIndexData.result.uv) }}
      </p>
    </div>
  </div>
<div>
    <h1 id="furtherCondTitle"> Golden hour </h1>
    <div id="blockGoldenHour">
        <p>Begins: {{dateFormat(new Date(uvIndexData.result.sun_info.sun_times.goldenHour))}}</p>
        <p>Ends: {{dateFormat(new Date(uvIndexData.result.sun_info.sun_times.goldenHourEnd))}}</p>
    </div>
    <p id="goldenHourPTag">* Golden hour is when the softest light occurs, the best time for photography</p>
</div>
  </div>
</template>

<script>
export default {
  name: "AdditionalInfo",
  data() {
    return {
      params: ["wavePeriod"],
      params2: ["sunrise", "sunset", "moonPhase"],
      weatherData: "",
      sunMoonData: "",
      tideData: "",
      uvIndexData: ""
    };
  },
  methods: {
    getEndTime() {
      let datetime = Math.round(new Date().getTime() / 1000); // gets new date/time
      return datetime + 86400 + 86400 + 86400; // adds 3 days in milisec to current date/time and updates timeframe
    },
    getStartTime() {
      let datetime = Math.round(new Date().getTime() / 1000);
      return datetime + 86400;
    },
    dateFormat(date) {
      return new Intl.DateTimeFormat("en-au", {
        hour: "numeric",
        minute: "numeric"
      }).format(date);
    }
  },
  mounted() {
    const headers = {
      Authorization:
        "411512a6-b996-11ea-9409-0242ac130002-41151364-b996-11ea-9409-0242ac130002",
        'x-access-token': 'bbeb7c535182ff31d69b52d5e1fc089f'
    };
    fetch(
      `https://api.stormglass.io/v2/weather/point?lat=${-33.890842}&lng=${151.274292}&params=${
        this.params
      }&start=${this.getStartTime()}&end=${this.getEndTime(144, 0)}`, // main api
      { headers }
    )
      .then(response => response.json())
      .then(data => (this.weatherData = data));

    fetch(
      `https://api.stormglass.io/v2/tide/extremes/point?lat=${-33.890842}&lng=${151.274292}&start=${this.getStartTime()}&end=${this.getEndTime(
        144,
        0
      )}`, // tide api
      { headers }
    )
      .then(response => response.json())
      .then(data => (this.tideData = data)),
      fetch(
        `https://api.stormglass.io/v2/astronomy/point?lat=${-33.890842}&lng=${151.274292}&start=${this.getStartTime()}&end=${this.getEndTime(
          144,
          0
        )}&params=${this.params2}`, // sunrise,sunset,moon phase api
        { headers }
      )
        .then(response => response.json())
        .then(data => (this.sunMoonData = data)),
      fetch(
        `https://api.openuv.io/api/v1/uv?lat=${-33.890842}&lng=${151.274292}`, // uv api
        { headers }
      )
        .then(response => response.json())
        .then(data => (this.uvIndexData = data));
  }
};
</script>

<style>
#furtherCondTitle {
  text-align: left;
  margin: 2vw;
  font-size: 18px;
}
#goldenHourPTag{
  text-align: left;
  margin: 2vw;
  font-size: 12px;
}
#blockOfConditions {
  display: flex;
  background: #fe7a66;
  border-radius: 5px;
  margin: 2vw;
  padding: 3vw;
  color: #fffffb;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

#blockGoldenHour{
  display: flex;
  background: #ffb45c;
  border-radius: 5px;
  margin: 2vw;
  padding: 3vw;
  color: #fffffb;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}
</style>