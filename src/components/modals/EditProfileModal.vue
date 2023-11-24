<template>
  <div id="edit">
    <!-- component -->
    <div class="flex flex-col items-center justify-center p-3 min-h-full">
      <button
          @click="onToggle"
          class="bg-purple-500 border border-purple-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-purple-600"
      >
        Update your profile
      </button>
    </div>
    <transition name="fade">
      <div v-if="isModalVisible">
        <div
            @click="onToggle"
            class="absolute bg-black opacity-70 inset-0 z-0"
        ></div>
        <div
            class="w-full max-w-lg p-3 relative mx-auto my-auto rounded-xl shadow-lg bg-white"
        >
          <div>
            <div class="p-3 flex-auto justify-center leading-6">
              <h2 class="text-center text-2xl font-bold py-4">Change your info</h2>
              <form class="mt-6">
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
              </form>
            </div>
            <div class="p-3 mt-2 text-center space-x-4 md:block">
              <button
                  class="mb-2 md:mb-0 bg-white px-5 py-2 text-sm shadow-sm font-medium tracking-wider border text-gray-600 rounded-md hover:shadow-lg hover:bg-gray-100"
                  @click="submit">
                Save
              </button>
              <button
                  @click="onToggle"
                  class="mb-2 md:mb-0 bg-purple-500 border border-purple-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-purple-600"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { useVuelidate } from '@vuelidate/core'
import { required,email } from '@vuelidate/validators'
import Swal from "sweetalert2";
export default {
  name: "EditProfileModal",
  setup: () => ({ v$: useVuelidate() }),
  data() {
    return {
      isOpen: false,
      show_error:false,
      user:[],
      form_data:{
        'name':'',
        'email':'',
      }
    };
  },

  computed: {
    isModalVisible() {
      return this.isOpen;
    }
  },

  methods: {
    onToggle() {
      this.isOpen = !this.isOpen;
    },
    async submit(e){
      e.preventDefault();
      if (this.checkSubmit()){
        console.log('submited')
        this.isOpen = !this.isOpen;
        this.$toast.success("Successfully saved",{position:"top-right"});
        this.form_data.name = '';
        this.form_data.email = '';
        // Submit form
        //  await axios
        //     .post("/admin/thirds", this.form_data)
        //     .then(function (response) {
        //       Swal.fire("Saved! Please login", "", "success");
        //       window.location.reload()
        //       // window.location.href = "/admin/thirds";
        //     })
        //     .catch(function (err) {
        //       try {
        //         Swal.fire("Something went wrong", "", "error");
        //       } catch (e) {
        //         Swal.fire("Something went wrong", "", "error");
        //       }
        //     });
      }else {
        await Swal.fire("Please fill form information", "", "info");
      }
    },
    checkSubmit(){
      this.v$.$touch()
      if (this.v$.form_data.name.$invalid || this.v$.form_data.email.$invalid) {
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
    }
  }

}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 500ms ease-out;
}

</style>