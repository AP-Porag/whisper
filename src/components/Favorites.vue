<template>
  <div class="latest_post">
    <div class="p-20 container">
      <h3 class="text-blue-300 mb-4 text-lg font-bold mb-20">
        Most Favorite
      </h3>
      <div class="m-auto grid grid-cols-1 md:grid-cols-2 gap-20">
        <Quote/>
      </div>
    </div>
  </div>
</template>

<script>
import Quote from "./partials/Quote.vue";

export default {
  name: "Favorites",
  components: {Quote}
}
</script>

<style scoped>
.latest_post {
  background: #1488cc;
  background: -webkit-linear-gradient(to right, #2b32b2, #1488cc);
  background: linear-gradient(to right, #2b32b2, #1488cc);
  font-family: "Fira Sans", sans-serif;

  //background-color: #37bdf8;
  //background-image: linear-gradient(147deg, #37bdf8 0%, rgba(3,3,196,1) 74%);
}
</style>