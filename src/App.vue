<template>
  <div id="app" :class="typeof weather.main!='undefined' && weather.main.temp>16 ?
    'warm' :'' ">
     <main>
       <div class="search-box">
       <input type="text" class="search-bar" 
       v-model="query"
       @keypress="fetchWeather"
       placeholder='search...'/>

       </div>
     <div class="weather-wrap" v-if="typeof weather.main !='undefined'">
       <div class="location-box">
         <div class="location">
{{weather.name}},{{weather.sys.country}}
<div class="date">{{dateBuilder()}}</div>
  
         </div>
       <div class="weather-box">
         <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
         <div class="weather">{{weather.weather[0].main}}</div>


       </div>
       </div>
   
     </div>
    </main>
    </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    return{
      api_key :'ed9dd5ce0b16546863c38d57bc544fe4',
url_base:'https://api.openweathermap.org/data/2.5/',
query:'',
weather:{}
    }
  },
  methods:{
    fetchWeather(e){
if(e.key=="Enter"){
fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
.then(res => 
{return res.json();

}).then(this.setResults);

  }
},
setResults(result){
  this.weather = result;
},
dateBuilder(){
  let d = new Date();
  let months =['january','february','march','april','May','June','July','August','September','October','November','December'];
let Days =['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'];
let date = d.getDate();
let month = months[d.getMonth()];
let day = Days[d.getDay()];
let year = d.getFullYear();
return `ITs ${day} ${date} ${month} ${year}`;
}


  }
}
</script>

<style>
  *{
    margin:0;
    padding:0;
    box-sizing:cover;
  }
  body{
    font-family:'montserrat',sans-serif;


  }
  main{
    min-height:100vh;
    padding:25px;
    background-image:linear-gradient(to bottom,rgba(0,0,0,0.25), rgba(0,0,0,0.75));
  }
  .search-box{
   width:100%;
   margin-bottom:30px;

  }
  .search-box .search-bar{
   width:90%;
   display:block;
   padding:30px;
   color:#313131;
   font-size:20px;
   border:none;
   appearance:none;
   outline:none;
   background:none;
   background-color:rgba(255,255,255,0.5);
   border-radius:0 16px 0 16px;
   transition:0.4s;
  }
.search-box .search-bar:focus{
  box-shadow:0 0 16px rgba(0,0,0,0.25);
  background-color:rgba(255,255,255,0.75);
  border-radius : 16px 0 16px 0;
  }
.location-box .location{
  text-align:center;
  font-size:30px;
  font-weight:500;
  color:#FFF;
  text-shadow: 1px 3px rgba(0,0,0,0.25);

}
.location-box .date{
    text-align:center;
  font-size:20px;
  font-weight: 300;
  font-style: italic;
  color:#FFF;
}
.weather-box{
  text-align:center;
}
.weather-box .temp{
  display:inline-block;
  padding: 10px 25px; 
  font-size: 102px;
  font-weight:900;
  color:#FFF;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius:16px;
  margin:30px 0;

}
.weather-box .weather{
color:#FFF;
font-size:48px;
font-weight:700;
font-style:italic;
text-shadow: 3px 6px rgba(0,0,0,0.25);
}


#app{
  background-image : url('./assets/img/flower.jpg');
  background-size:cover;
  background-position:bottom;
  background-repeat:no-repeat;
  transition:0.4s;
}


#app.warm{
  background-image : url("./assets/img/cold.jpg");

}
</style>
