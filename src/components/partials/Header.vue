<template>
  <header class="absolute inset-x-0 top-0 z-50">
    <nav class="flex items-center justify-between p-6 lg:px-8 " style="background: white;padding-right: 78px;padding-left: 78px" aria-label="Global">
      <div class="flex lg:flex-1">
        <router-link to="/" class="-m-1.5 p-1.5">
          <span class="sr-only">Whisper</span>
          <img class="h-8 w-auto" src="../../assets/vue.svg" alt="">
        </router-link>
        <span class="mt-1 ml-3 text-lg font-semibold uppercase" style="color: #37bdf8">Whisper</span>
      </div>
      <div class="flex lg:hidden">
        <button type="button" class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700" @click="showMobileNavbar = !showMobileNavbar">
          <span class="sr-only">Open main menu</span>
          <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
          </svg>
        </button>
      </div>
      <div class="hidden lg:flex lg:gap-x-12">
        <router-link to="/" class="text-sm font-semibold leading-6 text-gray-900">Home</router-link>
<!--        <router-link :to="user != null ? '/my-account/'+user[0].id : '/my-account'" class="text-sm font-semibold leading-6 text-gray-900" v-if="user != null">My Quotes</router-link>-->
        <router-link to="/my-account" class="text-sm font-semibold leading-6 text-gray-900" v-if="user != null">My Quotes</router-link>
      </div>
      <div class="hidden lg:flex lg:flex-1 lg:justify-end">
        <router-link to="/registration" class="text-sm font-semibold leading-6 text-gray-900 mr-5" v-if="user == null">Sign up <span aria-hidden="true"></span></router-link>
        <router-link to="/login" class="text-sm font-semibold leading-6 text-gray-900" v-if="user == null">Log in <span aria-hidden="true"></span></router-link>
        <button @click="logout"  class="text-sm font-semibold leading-6 text-gray-900" v-else>Log Out <span aria-hidden="true"></span></button>
      </div>
    </nav>
    <!-- Mobile menu, show/hide based on menu open state. -->
    <div class="lg:hidden" role="dialog" aria-modal="true" v-if="showMobileNavbar">
      <!-- Background backdrop, show/hide based on slide-over state. -->
      <div class="fixed inset-0 z-50"></div>
      <div class="fixed inset-y-0 right-0 z-50 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10">
        <div class="flex items-center justify-between">
          <router-link to="/" class="-m-1.5 p-1.5">
            <span class="sr-only">Whisper</span>
            <img class="h-8 w-auto" src="../../assets/vue.svg" alt="">
          </router-link>
          <span class="mt-1 ml-3 text-lg font-semibold uppercase" style="color: #37bdf8">Whisper</span>
          <button type="button" class="-m-2.5 rounded-md p-2.5 text-gray-700" @click="showMobileNavbar = !showMobileNavbar">
            <span class="sr-only">Close menu</span>
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/10">
            <div class="space-y-2 py-6">
              <router-link to="/" class="-mx-3 block rounded-lg px-3 py-2 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50">Home</router-link>
              <router-link to="/my-account" class="-mx-3 block rounded-lg px-3 py-2 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50" v-if="user != null">My Quotes</router-link>
            </div>
            <div class="py-6">
              <router-link to="/registration" class="-mx-3 block rounded-lg px-3 py-2.5 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50">Sign up</router-link>
              <router-link to="/login" class="-mx-3 block rounded-lg px-3 py-2.5 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50" v-if="user == null">Log in</router-link>
              <button @click="logout" type="button" class="-mx-3 block rounded-lg px-3 py-2.5 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50" v-else>Log out</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import axios from "axios";
import router from "../../router/index.js";
import Swal from "sweetalert2";

export default {
  name: "Header",
  data(){
    return{
      user: null,
      showMobileNavbar:false,
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

    logout(){
      // let self = this;
      console.log('clicked')

      axios.post("https://whisper.shadeofattire.com/api/logout")
          .then(function (response) {

            if (response.data.status == 200){
              // self.$toast.success('Successfully Logged out',{position:"top-right"})
              localStorage.setItem('user', null)
              self.user = null

              // window.location.reload();
              window.location.assign('https://ap-porag.github.io/whisper/');
              // router.push('/');
              // window.location.reload();
            }
          })
          .catch(function (err) {
            console.log(err)
            try {
              Swal.fire("Something went wrong", "", "error");
            } catch (e) {
              Swal.fire("Something went wrong", "", "error");
            }
          });
    }
  }
}
</script>

<style scoped>

</style>