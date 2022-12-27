<template>
  <Suspense>
    <template #default>
      <Weather />
    </template>
    <template #fallback>
      <Loading />
    </template>
  </Suspense>
</template>
  
<script>
import HelloWorld from './components/HelloWorld.vue'
import Weather from '@/components/Weather.vue'
import Test from '@/components/Test.vue'
import Loading from '@/components/LoadingFront.vue'
import ContentLoading from '@/components/ContentLoading.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Weather,
    Test,
    Loading,
    ContentLoading
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
