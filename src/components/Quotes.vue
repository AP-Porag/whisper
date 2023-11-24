<template>
  <div class="">
    <CreateQuoteModal/>
    <div class="p-20 container">
      <h3 class="text-blue-300 mb-4 text-lg font-bold mb-30" style="margin-bottom: 100px;">
        Latest Quotes
      </h3>
      <div class="m-auto grid grid-cols-1 md:grid-cols-2 gap-20">
        <Quote :id="1"/>
        <Quote :id="2"/>
      </div>
    </div>
  </div>
</template>

<script>
import Quote from "./partials/Quote.vue";
import CreateQuoteModal from "./modals/CreateQuoteModal.vue";

export default {
  name: "Quotes",
  components:{
    CreateQuoteModal,
    Quote
  }
}
</script>

<style scoped>
.latest_post {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  background: #1488cc;
  background: -webkit-linear-gradient(to right, #2b32b2, #1488cc);
  background: linear-gradient(to right, #2b32b2, #1488cc);
}
</style>