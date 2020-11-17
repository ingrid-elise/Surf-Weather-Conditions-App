<template>
  <div class="home">
    <CurrentDate />
    <div id="weatherIcon">
      <img id="sun-icon" alt="sun-icon" src="../assets/sunny.svg" />
    </div>
    <Heading msg="Hello, Bondi Beach" />
    <div id="todayFutureTitles">
      <!-- Titles for today, tomorrow, later buttons -->
      <button
        class="smallTitles"
        id="currentlyTitle"
        v-on:click="component = 'today'"
      >
        Today
      </button>

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
        v-on:click="component = 'later'"
      >
        Later
      </button>
    </div>
    <component :is="component"></component>
    <AdditionalInfo />
  </div>
</template>

<script>
// @ is an alias to /src
import Heading from "@/components/Heading.vue";
import CurrentDate from "@/components/CurrentDate.vue";
import WeatherDataBlocks from "@/components/WeatherDataBlocks.vue";
import TomorrowWeatherBlock from "@/components/TomorrowWeatherBlock.vue";
import LaterWeatherBlock from "@/components/LaterWeatherBlock";
import AdditionalInfo from "@/components/AdditionalInfo.vue";

export default {
  name: "Home",
  components: {
    Heading,
    CurrentDate,
    'today': WeatherDataBlocks,
    'tomorrow': TomorrowWeatherBlock,
    'later': LaterWeatherBlock,
    AdditionalInfo
  },
  data() {
    return {
      component: 'today',
    };
  },
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
