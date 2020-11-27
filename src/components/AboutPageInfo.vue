<template>
  <div id="about">
      <div id="intro">
          <h1>who are we?</h1>
          <div id="textAndImg">
      <p id="introText">
          How often do you spend waiting for ads to finish playing or avoiding whilst trying
          to monitor the surf conditions? For me, it wasn't what I needed at 6am on weekday
          trying to decide if slipping into the partially dry wetsuit was worth it for the waves.
          <br>
          As a creative and entrepreneurial pursuit I decided I would develop an add free, reliable
          platform to steamline what the waves were doing currently, later in the 
          day and for the following few days to give me the best low down on if the conditions were
          good, or to wait till later. 
          <br>
          As this is my first rodeo, feedback regarding the app is most welcome. 
        
      </p>
      <img src="../assets/Life is going to the a-ok.jpeg" alt="surfLife" id="imgLifeOk"> 
      </div>
      </div>
  </div>
</template>

<script>
export default {
    name: "AboutPageInfo",

}
</script>

<style>
#about {
    display: flex;
    flex-direction: column;
}
#intro {
     padding-left: 20vw;
     padding-right: 20vw;
     margin-top: 10vh;
}
h1 {
    padding: 20px;
}
#textAndImg {
    display: flex;
    flex-direction: row;
    justify-content: center;
}
#imgLifeOk{
    height: 45vh;
}
#introText {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>