<template>

<div id="app">

  <main>
    <div class="search-box">
      <input
       type="text"
        class="search-bar"
         placeholder="Search...."

         v-model="query"

         @keypress="fetchweather"
         
         />
        
    </div>
    <div class="weather-wrap">  

      <div class="location-box" v-if="typeof weather.main != 'undefined' ">
        <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
        <div class="date">{{datemaker()}}</div>
      </div>

      <div class="weather-box" v-if="typeof weather.main != 'undefined' ">
        <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
        <div class="weather">{{weather.weather[0].main}}</div>
      </div>
    </div>


  </main>
  

</div>
</template>

<script>


export default {
  name: 'App',

  data(){
    return{
      api_key: '494c7ca34121de75abe353f9708eea08',
      base_url: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }

  },

  methods: {

    fetchweather(e){
      if(e.key == "Enter"){
        fetch(`${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResult);
      }
    },

    setResult(results){
      this.weather = results;

    },
    datemaker(){

      let d = new Date();
      let months = ["January", "February", "March", 
      "April", "May", "June", "July", "August", "September",
      "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", 
      "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;

    }


    
  },


 
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;

}
body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('./assets/weather.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  background-repeat: no-repeat;
}

main{
  min-height: 100vh;
  padding: 30px;
}
.search-box{
  width: 100%;
  margin-bottom: 40px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 20px;
  color: #313131;
  font-size:16px;
  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px,rgba(0, 0, 0, 0.26);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;

}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.26);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: 500;

  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  margin-bottom: 20px;
  
  margin-top: 10px;
}

.weather-box .temp{
  display: inline-block;
  margin-bottom: 20px;
  padding: 12px 24px;
  color: #fff;
  font-size: 95px;
  font-weight: 800;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 15px;
  margin: 26px 0px;

  box-shadow: 3px 6px rgba(255, 255, 255, 0.25);
  margin: 0 auto;
}

.weather-box .weather{
  color: #fff;
  font-size: 50px;
  margin-top: 10px;
  font-weight: 800;
  font-style: italic;
  text-shadow: 3px 6px rgba(255, 255, 255, 0.25);
  margin: 0 auto;
}
</style>
