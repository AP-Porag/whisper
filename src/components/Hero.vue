<template>
  <div class="">
    <Header/>
    <HeroSlider/>
  </div>
</template>

<script>
import Header from "./partials/Header.vue";
import HeroSlider from "./partials/HeroSlider.vue";

export default {
  name: "Hero",
  components: {HeroSlider, Header},
  data () {
    return {}
  }
}
</script>

<style scoped>

</style>