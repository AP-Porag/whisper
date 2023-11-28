<template>
  <section class="flex flex-col md:flex-row h-screen items-center">

    <div class="bg-indigo-600 hidden lg:block w-full md:w-1/2 xl:w-2/3 h-screen">
      <img src="https://source.unsplash.com/random" alt="" class="w-full h-full object-cover">
    </div>

    <div class="bg-white w-full md:max-w-md lg:max-w-full md:mx-auto md:mx-0 md:w-1/2 xl:w-1/3 h-screen px-6 lg:px-16 xl:px-12
        flex items-center justify-center">

      <div class="w-full h-100">


        <h1 class="text-xl md:text-2xl font-bold leading-tight mt-12">Log in to your account</h1>

        <form class="mt-6">
          <div>
            <label class="block text-gray-700">Email Address</label>
            <input type="email" name="" id="" placeholder="Enter Email Address" class="w-full px-4 py-3 rounded-lg bg-gray-200 mt-2 border focus:border-blue-500 focus:bg-white focus:outline-none" autofocus autocomplete v-model.trim="v$.form_data.email.$model">
            <div class="text-red-500" v-if="v$.form_data.email.required.$invalid && show_error">
              Email is required
            </div>
            <div class="text-red-500" v-if="v$.form_data.email.email.$invalid && show_error">
              Give A valid email
            </div>
          </div>

          <div class="mt-4">
            <label class="block text-gray-700">Password</label>
            <input type="password" name="" id="" placeholder="Enter Password" minlength="6" class="w-full px-4 py-3 rounded-lg bg-gray-200 mt-2 border focus:border-blue-500
                focus:bg-white focus:outline-none" v-model.trim="v$.form_data.password.$model">
            <div class="text-red-500" v-if="v$.form_data.password.required.$invalid && show_error">
              Password is required
            </div>
          </div>

          <button @click='submit' class="w-full block bg-indigo-500 hover:bg-indigo-400 focus:bg-indigo-400 text-white font-semibold rounded-lg
              px-4 py-3 mt-6">Log In</button>
        </form>

        <p class="mt-8">Need an account? <router-link to="/registration" class="text-blue-500 hover:text-blue-700 font-semibold">Create an
          account</router-link></p>


      </div>
    </div>

  </section>
</template>

<script>
import Swal from 'sweetalert2'
import axios from 'axios'
import { useVuelidate } from '@vuelidate/core'
import { required,email } from '@vuelidate/validators'
import router from "../router/index.js";
export default {
  name: "LoginView",
  setup: () => ({ v$: useVuelidate() }),
  data(){
    return{
      show_error:false,
      user:[],
      isLoggedIn:false,
      form_data:{
        email:'',
        password:'',
      }
    }
  },
  methods:{
    async submit(e){
      let self = this;
      e.preventDefault();
      if (this.checkSubmit()){

        // Submit form
        await axios
            .post("http://whisper-admin.test/api/login", this.form_data)
            .then(function (response) {

              if (response.data.status == 200){
                self.$toast.success('Successfully Logged in',{position:"top-right"})
                self.user.push(response.data.data)
                localStorage.setItem('user', JSON.stringify(self.user))
                self.isLoggedIn = true;

                self.form_data.email = '';
                self.form_data.password = '';

                window.location.reload();
                // router.push('/');
              }else {
                Swal.fire("Wrong credentials!", "", "error");
              }
              // window.location.reload()
              // window.location.href = "/admin/thirds";
              router.push('/');
              // window.location.reload();
            })
            .catch(function (err) {
              console.log(err)
              try {
                Swal.fire("Something went wrong", "", "error");
              } catch (e) {
                Swal.fire("Something went wrong", "", "error");
              }
            });
      }else {
        await Swal.fire("Please give your credentials", "", "info");
      }
    },
    checkSubmit(){
      this.v$.$touch()
      if (this.v$.form_data.email.$invalid || this.v$.form_data.password.$invalid) {
        this.show_error = true;
        return false;
      }
      return true;
    },
  },
  validations: {
    form_data: {
      email: {
        required,
        email
      },
      password: {
        required,
      },
    }
  }
}
</script>

<style scoped>

</style>