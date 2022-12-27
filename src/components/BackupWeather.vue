<template>
    <div class="weather">
      <input type="text" v-model="findCityOne" v-on:keyup.enter="clickMe()">
      {{ result.id }},
      {{ result.name }},
      {{ result.sys?.country }}.
      {{ result.weather[0]?.description }},
      {{ unixtimestampdate }}
      {{ unixtimestamptime }}
      <img :src="displayImg" alt="">
    </div>
  </template>
  
  <script>
  import { ref, computed, onMounted } from "vue";
  import moment from 'moment'
  
  export default {
    async setup() {
      const result = ref([])
      const findCity = ref('Jakarta')
      const findCityOne = ref('')
      const weatherTemp = ref({})
      const url_base = ref('https://api.openweathermap.org/data/2.5/')
      const api_key = ref('20f24096c9b06b35d10c50d671497829')
      const url_img = ref('http://openweathermap.org/img/wn/')
      const unixtimestampdate = ref('')
      const unixtimestamptime = ref('')
      const lat = ref(0)
      const lon = ref('')
      const dateSettings = ref({
        weekday: "long",
        year: "numeric",
        month: "long",
        day: "numeric",
        // hour: 'numeric',
        // minute: 'numeric',
        // second: 'numeric'
      })
      
      const weatherAPI = async() => {
        try {
          if (findCity.value.length > 0) {
            const resultResponse = await fetch(`${url_base.value}weather?q=${findCity.value}&units=metric&appid=${api_key.value}&lang=id&{lat}&lon={lon}`)
            result.value = await resultResponse.json()
            console.log(result.value)
          }
        } catch (error) {
          console.log("ERROR")
        }
      }
  
      await weatherAPI()
  
      function clickMe() {
        findCity.value = findCityOne.value
        weatherAPI()
        findCityOne.value = ''
      }
  
      const displayImg = computed(() => `${url_img.value}${result.value.weather[0].icon}@2x.png`)
  
      function getDate() {
        // unixtimestampdate.value = new Date(result.value.dt * 1000).toLocaleDateString('id-ID',dateSettings.value)
        var timezone = result.value.timezone //needs to be converted in minutes 
        var timezoneInMinutes = timezone / 60;
        // unixtimestamptime.value = moment().utcOffset(timezoneInMinutes).format("h:mm:ss A");
        unixtimestampdate.value = moment().locale('id').utcOffset(timezoneInMinutes).format("dddd, LL");
        // console.log(unixtimestamptime.value)
      }
  
      getDate()
  
      setInterval(() => {
        getDate()
      }, 1000);
  
      function getTime() {
        var timezone = result.value.timezone //needs to be converted in minutes 
        var timezoneInMinutes = timezone / 60;
        // unixtimestamptime.value = moment().utcOffset(timezoneInMinutes).format("h:mm:ss A");
        unixtimestamptime.value = moment().utcOffset(timezoneInMinutes).format("HH:mm:ss");
        // console.log(unixtimestamptime.value)
      }
  
      getTime()
  
      setInterval(() => {
        getTime()
      }, 1000);
  
      lat.value = navigator.geolocation.getCurrentPosition((position) => {
        position.coords.latitude, position.coords.longitude;
      });
  
      console.log(lat.value)
  
      onMounted(() => {
        lon.value = "TEST123"
      })
  
      console.log(lon.value)
  
      // onMounted(() => console.log("UNMOUNTED"))
      
          return {
           result,
           findCity,
           findCityOne,
           url_base,
           api_key,
           weatherTemp,
           url_img,
           displayImg,
           dateSettings,
           unixtimestampdate,
           unixtimestamptime,
           lat,
           lon,
           clickMe
          }
      }
  }
  </script>
  
  <style>
  
  </style>