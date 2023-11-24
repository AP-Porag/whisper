<template>
  <div class="latest_post">
    <div class="p-20 container">
      <h3 class="text-blue-300 mb-4 text-lg font-bold mb-20" style="margin-bottom: 100px;">
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

</style>