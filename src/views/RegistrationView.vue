<template>
  <section class="flex flex-col md:flex-row h-screen items-center">

    <div class="bg-indigo-600 hidden lg:block w-full md:w-1/2 xl:w-2/3 h-screen">
      <img src="https://source.unsplash.com/random" alt="" class="w-full h-full object-cover">
    </div>

    <div class="bg-white w-full md:max-w-md lg:max-w-full md:mx-auto md:mx-0 md:w-1/2 xl:w-1/3 h-screen px-6 lg:px-16 xl:px-12
        flex items-center justify-center">

      <div class="w-full h-100">


        <h1 class="text-xl md:text-2xl font-bold leading-tight mt-12">Create your account</h1>

        <form class="mt-6" action="#" method="POST">
          <div>
            <label class="block text-gray-700">Name</label>
            <input type="text" name="" id="" placeholder="Enter your name" class="w-full px-4 py-3 rounded-lg bg-gray-200 mt-2 border focus:border-blue-500 focus:bg-white focus:outline-none" autofocus autocomplete v-model.trim="v$.form_data.name.$model">
            <div class="text-red-500" v-if="v$.form_data.name.required.$invalid && show_error">
              Name is required
            </div>
          </div>

          <div class="mt-4">
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

          <button class="w-full block bg-indigo-500 hover:bg-indigo-400 focus:bg-indigo-400 text-white font-semibold rounded-lg
              px-4 py-3 mt-6" @click="submit">Sign In</button>
        </form>

        <p class="mt-8">Already have an account? <router-link to="/login" class="text-blue-500 hover:text-blue-700 font-semibold">Login</router-link></p>


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
  name: "RegistrationView",
  setup: () => ({ v$: useVuelidate() }),

  data(){
    return{
      show_error:false,
      form_data:{
        'name':'',
        'email':'',
        'password':''
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
            .post("https://whisper.shadeofattire.com/api/registration", self.form_data)
            .then(function (response) {

              if (response.data.status == 200){
                Swal.fire("Saved! Please login", "", "success");
                self.form_data.name = '';
                self.form_data.email = '';
                self.form_data.password = '';

                router.push('/login');
              }else {
                Swal.fire(response.data.message, "", "error");
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
      }else {
        await Swal.fire("Please fill form information", "", "info");
      }
    },
    checkSubmit(){
      this.v$.$touch()
      if (this.v$.form_data.name.$invalid || this.v$.form_data.email.$invalid || this.v$.form_data.password.$invalid) {
        this.show_error = true;
        return false;
      }
      return true;
    },
  },
  validations: {
    form_data: {
      name: {
        required,
      },
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