<template>
  <div class="container">
    <div class="container-header">
      <h1>
        The Weather App
      </h1>
      <input type="text" class="newCity" placeholder="Enter your city" v-model="city">
      <input type="text" class="newCity" placeholder="Enter your country" v-model="country">
      <button v-on:click="getWeather">Get your weather</button>
    </div>

<!-- boucle pour choper 1 info sur 8 -->
    <div v-for="(d, index) in forecastArray" v-if="index %8===0" :key="d.id">
      <div>Minimum Temperature: {{d.main.temp_min}}</div>
      <div>Maximum Temperature: {{d.main.temp_max}}</div>
      <div>Description: {{d.weather[0].description}}</div>
      <img v-bind:src="'http://openweathermap.org/img/w/'+getIcon(d.weather[0].icon)" alt="icone météorologique">
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
          city:'',
          country:'',
          forecastArray:'',
      }
    },

    methods: {
      getWeather(){
        var key = "8294542c24bda3ed6691a82de8189445"; // ma clef pour accéder à l'API
        var url="https://api.openweathermap.org/data/2.5/forecast";
        url+="?q="+this.city+","+this.country; // cherche la ville et le pays choisis par l'utilisateur
        url+="&units=metric"; // précise l'unité en degré celcius
        url+="&APPID="+key; // mentionne ma clef
        url+="&mode=json"; // précise le langage en json

        fetch(url)
        .then(resp => { return resp.json() })
        .then(all => {
          this.forecastArray = all.list;
        })
        .catch(function() {
          // catch any errors
        })
      },

      getIcon:function(icon) {
        return icon+'.png'
      }
    }
  }
</script>

<style scoped>


</style>
