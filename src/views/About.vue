<template>
  <div class="about">
    <AboutPageInfo />
  </div>
</template>

<script>
import AboutPageInfo from "@/components/AboutPageInfo"

export default {
  name: "About",
  components: {
    AboutPageInfo,
  }
}
</script>

<style >
* {
  margin: 0;
  padding: 0;
}

#about {
    height: 100vh;
    background-color: #38505c;
    color: white;
}
</style>
