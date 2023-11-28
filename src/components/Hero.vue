<template>
  <div class="">
<!--    <Header/>-->
    <HeroSlider/>
    <CreateQuoteModal v-if="user != null" :user="user[0]"/>
  </div>
</template>

<script>
// import Header from "./partials/Header.vue";
import HeroSlider from "./partials/HeroSlider.vue";
import CreateQuoteModal from "./modals/CreateQuoteModal.vue";

export default {
  name: "Hero",
  components: {
    CreateQuoteModal, HeroSlider,
    // Header
  },
  data () {
    return {
      user:null
    }
  },
  created() {
    this.getLocalUser();
  },
  methods:{
    async getLocalUser(){
      let user = JSON.parse(localStorage.getItem('user')) || null;
      console.log(user)

      if (user == 'undefined'){
        console.log('undefineds')
      }else {
        console.log('undefineds')
        this.user = user;
        console.log(this.user[0].id)
      }
    },
  }
}
</script>

<style scoped>

</style>