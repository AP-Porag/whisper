<template>
<!--  <div class="p-20 bg-blue-100">-->
  <div class="p-20">
    <h3 class="text-blue-300 mb-4 text-md font-bold">
      Latest Quotes
    </h3>
    <Quote/>
  </div>
</template>

<script>
import Quote from "./partials/Quote.vue";

export default {
  name: "Quotes",
  components:{
    Quote
  }
}
</script>

<style scoped>

</style>