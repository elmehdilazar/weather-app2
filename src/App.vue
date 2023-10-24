<template>
<div class="app">
  <div class="header container h-100 p-5">
    <h1 class="mb-5">Weather App</h1>
    <div class="d-flex justify-content-center h-100">

<div class="searcbar w-50 mx-2">
  <input type="text" class="input form-control" v-model="city" placeholder="Enter a City">
</div>
<button type="button" class="btn-search btn btn-primary" @click="searchWeather">Search <i class="fa fa-search" aria-hidden="true"></i></button>

    </div>
  </div>
</div>
<br>
<weather :city="city" v-if="showWeather"></weather>
</template>
<script>
import Weather from './components/Weather.vue';
export default {
  name: "App",
  components: {Weather},
  data() {
    return {
      city: "",
      showWeather:false,
    }
  },
  methods: {
    async searchWeather() {
      this.showWeather = false;
      await this.$nextTick();
      this.showWeather = true;
    }
  },
}
</script>
<style lang="scss">
body{
  background-color: #121212 !important;

}
.header{
  background-color: #212730;
  border-radius: 20px;
  margin-top: 5rem;
  color: #fff;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  text-align: center;
}
.btn-search{
  background-image: linear-gradient(to right,cyan,magenta);
}
</style>
