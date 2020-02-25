<template>
    <div>
        <h1>Weather</h1>
    </div>
</template>

<script>
import axios from "axios";
export default {
    
      data() {
    return {

    };
  },
    methods:{
            getWeather() {
      axios
        .get(
          `http://localhost:5000/weather`
        )
        .then(response => {
            console.log(response);
        })
        .catch(error => {
          console.error(error);
        });
    },
    },
    created() {
        this.getWeather();
    }
}
</script>

<style lang="scss">

</style>