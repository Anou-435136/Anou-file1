<template>
  <div class="about">
    <div class="weather">
      <h1 class="weather-title">{{name}}の天気情報</h1>
      <ul>
        <li>天気:{{main}}</li>
        <li>温度:{{temp}}℃</li>
        <li>湿度:{{humidity}}%</li>
        <li>風速:{{speed}}m</li>
      </ul>
      <a @click="$router.push({name: 'Home'})" class="btn">button</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["city"],
  data() {
    return {
      name: "",
      main: "",
      temp: "",
      humidity: "",
      speed: ""
    };
  },
  async created() {
    let item = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city},jp&units=metric&appid=859a161d3ffaa949286d233a6c83ba4f`);

    this.data = item.data;
    this.name = this.data.name;
    this.main = this.data.weather[0].main;
    this.temp = this.data.main.temp;
    this.humidity = this.data.main.humidity;
    this.speed = this.data.wind.speed;
  }
};
</script>

<style scoped>
.about {
  width: 100vw;
  height: 100vh;
  background-image: url("https://coachtech-video.s3-ap-northeast-1.amazonaws.com/liane-metzler-Y1ByvAGQ5iE-unsplash+(1).jpg");
  background-size: cover;
  color: white;
}

.weather {
  width: 620px;
  margin: 0 auto;
  padding-top: 100px;
}

.weather-title {
  font-size: 64px;
}

.weather li {
  font-size: 24px;
  margin: 20px 0 0 30px;
}

.btn {
  display: block;
  width: 600px;
  margin-top: 50px;
  padding: 10px;
  text-align: center;
  text-decoration: none;
  color: #ec407a;
  border: 2px solid #ec407a;
  border-radius: 3px;
  transition: 0.4s;
  cursor: pointer;
}

.btn:hover {
  background: #ec407a;
  color: #fff;
}
</style>