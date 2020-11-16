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

<style scoped>
#about {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 20vw;
}
</style>
