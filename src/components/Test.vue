<template>
  <h1>YOUR COORDINATES:</h1>
    <p>Lat: {{ coords.lat }}, Lang: {{ coords.lang }}</p>
</template>

<script>

export default {
    data() {
      return {
        coords: {
          lat: '',
          long: ''
        }
      }
    },
    created() {
      this.$getLocation(options)
      .then(coordinates => {
        this.coords = coordinates
      });
    }
}
</script>

<style>

</style>