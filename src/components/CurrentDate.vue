<template>
<div id="currentDate">
    <p id="timestamp">{{timestamp}}</p>

    </div>
  
</template>

<script>
export default {
    name: "CurrentDate",
    data() {
        return {
         timestamp: '',
        }
    },
    created() {
        setInterval(this.getNow, 1000);
    },
    methods: {
        getNow: function() {
        const today = new Date();
        var day = today.getDay(); 
        var weekday = new Array(7);
        weekday[0] = "Sunday";
        weekday[1] = "Monday";
        weekday[2] = "Tuesday";
        weekday[3] = "Wednesday";
        weekday[4] = "Thursday";
        weekday[5] = "Friday";
        weekday[6] = "Saturday";
        var dayToday = weekday[today.getDay()];
        var date = dayToday+', '+today.getDate()+'/'+(today.getMonth()+1)+'/'+today.getFullYear();

        const dateTime = date;
        this.timestamp = dateTime; 
    },
    },
   
}

</script>

<style>
#timestamp {
    display: flex;
    flex-direction: row;
    font-size: 0.7rem;
    justify-content: flex-end;
    width: 95%;
}
</style>