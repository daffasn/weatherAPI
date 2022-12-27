<template>
  <div class="weather bg-gradient-to-r from-purple-500 to-pink-500 text-slate-50 h-screen">
    <div class="flex justify-center items-center h-screen">
      <!-- <div class="border-solid border-transparent border-sky-500 shadow-[10px_20px_20px_10px_#00000024] p-4 rounded-lg backdrop-filter backdrop-blur-sm bg-opacity-0 max-w-screen-sm md:max-w-lg bg-[length:750px_650px] bg-center"> -->
      <div v-if="contentLoading">
        <div v-if="typeof result.name =='undefined'">
          <div class="border-solid border-transparent border-sky-500 p-4 rounded-lg max-w-lg md:w-[32rem] shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.38)]">
            <div>
              <input class="w-full h-10 rounded-md text-white text-2xl p-2 backdrop-blur-sm bg-white/10 outline-white" type="text" placeholder="Search here..." v-model="findCityOne" v-on:keyup.enter="clickMe()">
            </div>
            <div class="mt-8 text-center border-solid border-2 border-transparent rounded-lg backdrop-blur-sm bg-white/0 text-black text-2xl shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.68)] text-shadow">
              <h1 class="text-5xl">NOT FOUND</h1>
            </div>
            </div>
        </div>
        <div v-else>
          <div v-if="unixtimestamptime <= unixtimestampsunset && unixtimestamptime >= unixtimestampsunrise">
            <div class="border-solid border-transparent border-sky-500 p-4 md:rounded-lg bg-[url('@/assets/siang.png')] bg-[length:850px_750px] md:bg-[length:550px_480px] w-screen md:w-[32rem] h-screen md:h-full shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.38)] flex flex-col justify-center">
              <!-- <div class="border-solid border-transparent border-sky-500 p-4 md:rounded-lg bg-[url('@/assets/night4.jpg')] bg-[length:850px_750px] bg-center max-w-lg md:w-[32rem] h-screen shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.38)] flex flex-col justify-center"> -->
              <div>
                <input class="w-full h-10 rounded-md text-white text-2xl p-2 backdrop-blur-sm bg-white/10 outline-white" type="text" placeholder="Search here..." v-model="findCityOne" v-on:keyup.enter="clickMe()">
              </div>
              <div class="mt-8 text-center border-solid border-2 border-transparent rounded-lg backdrop-blur-sm bg-white/0 text-black text-2xl shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.68)] text-shadow" :style="{color:changeColor, textShadow: changeTextShadow}">
                <div v-if="result.name.length >= 29">
                  <h1 class="text-4xl">{{ result.name }}, {{ result.sys?.country }}.</h1>
                </div>
                <div v-else>
                  <h1 class="text-5xl">{{ result.name }}, {{ result.sys?.country }}.</h1>
                </div>
                <h1>{{ unixtimestampdate }}</h1>
                <h1>{{ unixtimestamptime }}</h1>
              </div>
              <div class="flex justify-between items-center mt-2" :style="{color:changeColor, textShadow: changeTextShadow}">
                <img :src="displayImg" alt="" class="   h-44">
                <h1 class="text-7xl text-shadow">{{ Math.round(result.main.temp) }}°C</h1>
              </div>
              <div class="flex justify-between text-xl font-bold" :style="{color:changeColor, textShadow: changeTextShadow}">
                <h1 class="capitalize text-shadow">{{ result.weather[0]?.description }}</h1>
                <h1 class="text-shadow">Berasa seperti {{ Math.round(result.main.feels_like) }}°C</h1>
              </div>
              </div>
        </div>
        <div v-else>
              <div class="border-solid border-transparent border-sky-500 p-4 md:rounded-lg bg-[url('@/assets/night4.jpg')] bg-[length:850px_750px] md:bg-[length:550px_480px] max-w-lg md:w-[32rem] h-screen md:h-full shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.38)] flex flex-col justify-center">
              <!-- <div class="border-solid border-transparent border-sky-500 p-4 md:rounded-lg bg-[url('@/assets/night4.jpg')] bg-[length:850px_750px] bg-center max-w-lg md:w-[32rem] h-screen shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.38)] flex flex-col justify-center"> -->
              <div>
                <input class="w-full h-10 rounded-md text-white text-2xl p-2 backdrop-blur-sm bg-white/10 outline-white" type="text" placeholder="Search here..." v-model="findCityOne" v-on:keyup.enter="clickMe()">
              </div>
              <div class="mt-8 text-center border-solid border-2 border-transparent rounded-lg backdrop-blur-sm bg-white/0 text-black text-2xl shadow-[4.0px_8.0px_8.0px_rgba(0,0,0,0.68)] text-shadow" :style="{color:changeColor, textShadow: changeTextShadow}">
                <div v-if="result.name.length >= 29">
                  <h1 class="text-4xl">{{ result.name }}, {{ result.sys?.country }}.</h1>
                </div>
                <div v-else>
                  <h1 class="text-5xl">{{ result.name }}, {{ result.sys?.country }}.</h1>
                </div>
                <h1>{{ unixtimestampdate }}</h1>
                <h1>{{ unixtimestamptime }}</h1>
              </div>
              <div class="flex justify-between items-center mt-2" :style="{color:changeColor, textShadow: changeTextShadow}">
                <img :src="displayImg" alt="" class="   h-44">
                <h1 class="text-7xl text-shadow">{{ Math.round(result.main.temp) }}°C</h1>
              </div>
              <div class="flex justify-between text-xl font-bold" :style="{color:changeColor, textShadow: changeTextShadow}">
                <h1 class="capitalize text-shadow">{{ result.weather[0]?.description }}</h1>
                <h1 class="text-shadow">Berasa seperti {{ Math.round(result.main.feels_like) }}°C</h1>
              </div>
              </div>
        </div>
        </div>
      </div>
      <div v-else>
        <Loading />
      </div>
      
    </div>
  </div>
</template>

<script>
import { ref, computed, watchEffect } from "vue";
import moment from 'moment'
import Loading from '@/components/ContentLoading.vue'

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
    const unixtimestampsunset = ref('')
    const unixtimestampsunrise = ref('')
    const contentLoading = ref(true)
    const dateSettings = ref({
      weekday: "long",
      year: "numeric",
      month: "long",
      day: "numeric",
      // hour: 'numeric',
      // minute: 'numeric',
      // second: 'numeric'
    })
    
    const weatherAPIWithPermissions = async(position) => {
    try {
      if (position.coords.latitude.length != 0 && position.coords.longitude.length != 0 && findCity.value.length > 0) {
        const resultResponse = await fetch(`${url_base.value}weather?lat=${position.coords.latitude}&lon=${position.coords.longitude}&units=metric&appid=${api_key.value}&lang=id`)
        result.value = await resultResponse.json()
      }
      console.log(result.value)
    } catch (error) {
      console.log("ERROR")
    }
  }
  
  const weatherAPI = async() => {
    try {
        if (findCity.value.length > 0) {
          const resultResponse = await fetch(`${url_base.value}weather?q=${findCity.value}&units=metric&appid=${api_key.value}&lang=id`)
          result.value = await resultResponse.json()
        } 
        console.log(result.value)
      } catch (error) {
        console.log("ERROR")
      }
    }

    navigator.geolocation.getCurrentPosition(weatherAPIWithPermissions, weatherAPI);

    await weatherAPI()

    function clickMe() {
      findCity.value = findCityOne.value
      weatherAPI()
      loadingContent()
      findCityOne.value = ''
    }

    const displayImg = computed(() => `${url_img.value}${result.value.weather[0].icon}@4x.png`)

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

    watchEffect(() => {
      unixtimestampsunset.value = moment.utc((result.value.sys.sunset + result.value.timezone) * 1000).format('HH:mm')
      // console.log(unixtimestampsunset.value)

      unixtimestampsunrise.value = moment.utc((result.value.sys.sunrise + result.value.timezone) * 1000).format('HH:mm')
      // console.log(unixtimestampsunrise.value)
    })

    const changeColor = computed(() => {
      if (unixtimestamptime.value <= unixtimestampsunset.value && unixtimestamptime.value >= unixtimestampsunrise.value) {
        return 'white'
      } else {
        return 'black'
      }
    })

    const changeTextShadow = computed(() => {
      if (unixtimestamptime.value <= unixtimestampsunset.value && unixtimestamptime.value >= unixtimestampsunrise.value) {
        return '2px 2px 5px #000'
      } else {
        return '2px 2px 5px #FFF'
      }
    })

    function loadingContent() {
      contentLoading.value = false
      setTimeout(() => contentLoading.value = true, 3000)
    }

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
         unixtimestampsunset,
         unixtimestampsunrise,
         clickMe,
         changeColor,
         changeTextShadow,
         contentLoading,
         loadingContent
        }
    },
    components: {
      Loading
    }
}
</script>

<style scoped>
/* .weather{
  background-image: url('@/assets/logo.png');
} */
@import url('https://fonts.googleapis.com/css2?family=Play&display=swap');
.weather {
  /* font-family: 'Space Grotesk', sans-serif; */
  /* font-family: 'Covered By Your Grace', cursive; */
  /* font-family: 'Aldrich', sans-serif; */
  font-family: 'Play', sans-serif;
}
</style>