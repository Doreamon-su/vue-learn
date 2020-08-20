<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <slider-confirm id="slider-confirm"></slider-confirm>
  </div>
</template>

<script>
// @ is an alias to /src
import SliderConfirm from "../components/SliderConfirm.vue"

export default {
  name: 'Home',
  components: {
    SliderConfirm
  }
}
</script>
<style scoped>
#slider-confirm{
position: absolute;
left: 300px;
}
</style>
