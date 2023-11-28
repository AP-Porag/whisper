<template>
<div class="">
  <hero/>
  <Quotes/>
  <Favorites/>
</div>
</template>

<script>
import Hero from '../components/Hero.vue'
import Quotes from "../components/Quotes.vue";
import Favorites from "../components/Favorites.vue";
export default {
  name: "HomeView",
  components:{
    Favorites,
    Quotes,
    Hero,
  },
}
</script>

<style scoped>

</style>