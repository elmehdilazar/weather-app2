<template>
  <div class="container p-0">
    <div class="d-flex ph">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">{{ day}}</h2>
          <p class="text-light date mb-0">{{date}}</p>
          <small>{{time}}</small>
          <h2 class="place">
            <i class="fas fa-location">{{ name }} <small>{{country}}</small></i>
          </h2>
          <div class="temp">
            <h1 class="weather-temp">{{temperature}}&deg;</h1>
            <h2 class="text-light">{{description}} <img :src="iconurl"></h2>
          </div>
        </div>
      </div>
      <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Sea Level</th>
              <td>{{ sea_level }}</td>
            </tr>
            <tr>
              <th> humidity </th>
              <td>{{ humidity }}</td>
            </tr>
            <tr>
              <th>wind</th>
              <td>{{ wind }}</td>
            </tr>
          </tbody>
        </table>
        <days-weather :cityname="cityname"></days-weather>
        <div id="div_form" class="d-flex m-3 justify-content-center">
          <form action="" class="text-center">
            <input
            @click="changeLocation"
              type="text"
              value="Change Location"
              class="btn change-btn btn-primary"
            />
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import DaysWeather from "./DaysWeather.vue";
export default {
  components: { DaysWeather },
  name: "Weather",
  props: {
    city: String,
  },
  data() {
    return {
      day: null,
cityname:this.city,
      temperature: null,
      description: null,
      iconurl: null,
      date: null,
      time: null,
      name: null,
      country:null,
      wind: null,
      sea_level: null,
      humidity: null,
      
      monthNames: ["January", "February", "March", "April", "May", "June", "July", "August"
        , "September", "October", "November", "December"],
      //days name
      daysName: [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday",
        ],
    
        
    };
  },
  methods: {
    changeLocation() {
      window.location.reload();
    }
  },

  async created() {
    const response = await axios.get(
      `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=5165e738fc14279c38d921614426c7bc`
    );
    const weatherData = response.data;
    this.temperature =Math.round(weatherData.main.temp);
    this.description = weatherData.weather[0].description;
    this.iconurl = `http://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
    this.name = weatherData.name;
    const d = new Date();
    this.day =this.daysName[d.getDay()];
    this.date = d.getDate() + '-' + this.monthNames[d.getMonth()] + '-' + d.getFullYear();
    this.time = d.getHours() + ":" + d.getMinutes() + ":" + d.getSeconds();
    this.country = weatherData.sys.country;
    this.wind = Math.round(weatherData.wind.speed);
    this.sea_level = Math.round(weatherData.main.pressure);
     this.humidity = Math.round(weatherData.main.humidity) ;
    

    // console.log(weatherData);
  },
};
</script>
<style>
body {
  background-color: #343d4b;
}
.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
}
h2.mb-1.day {
  font-size: 3rem;
  font-weight: 400;
}
.main-div {
  border-radius: 20px !important;
  color: #fff !important;
  background-image: url("https://images.unsplash.com/photo-1502758185688-8f322e06d0eb?auto=format&fit=crop&q=80&w=1470&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D");
  background-size: cover;
  background-position: center;
  background-blend-mode: overlay !important;
  background-color: rgba(0, 0, 0, 0.5) !important;
  background-repeat: no-repeat;
}
.temp {
  position: absolute;
  bottom: 0;
}
.main-div:hover {
  transform: scale(1.1);
  transition: transform 0.5 ease;
  z-index: 1;
}
.card-2 {
  background-color: #212730 !important;
  border-radius: 20px !important;
}
.card-details {
  margin-left: 19px;
}
.h1_Left {
  position: absolute;
  bottom: 25px;
  left: 16px;
  font-size: "vw";
  line-height: 1.2;
}
.h3_Left {
  position: absolute;
  left: 16px;
  font-size: 2vw;
  line-height: 0.5;
}
.h3_Left small {
  font-size: 1rem;
}
table {
  position: relative;
  left: 15px;
  border-collapse: separate;
  border-spacing: 15px;
  width: 85%;
  text-align: left;
  max-width: 600px;
  margin: 0 auto;
}
th,
td {
  font-size: 18px;
  color: #fff;
}
td {
  text-align: right;
}
table,
tr:hover {
  color: red;
}
.change-btn {
  background-image: linear-gradient(to right, cyan, magenta);
}
.change-btn:hover {
  transform: scale(0.9);
  transition: transform 0.1 ease;
}
@media (max-width: 430px) and (min-width: 290px){
.d-flex.ph {
    flex-direction: column;
    display: flex !important;
}
.days>.li_active>div{
  font-size: 14px;
}
.main-div{
  height: 300px !important;
}
}
</style>
