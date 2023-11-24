<template>
  <div id="app">
    <div class="flex flex-row items-center justify-center p-3 min-h-full">
      <button
          @click="onToggle"
          class="bg-purple-500 border border-purple-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-purple-600"
      >
        Open
      </button>
    </div>
    <transition name="fade">
      <div v-if="isModalVisible">
        <div
            @click="onToggle"
            class="absolute bg-black opacity-70 inset-0 z-0"
            style="z-index: 102"
        ></div>
        <div
            class="w-full max-w-lg p-3 relative mx-auto my-auto rounded-xl shadow-lg bg-white"
            style="z-index: 1000">
          <div>
            <div class="p-3 flex-auto justify-center leading-6">
              <h2 class="text-center text-2xl font-bold py-4">Create Quote</h2>
              <form class="mt-6">
                <div>
                  <label class="block text-gray-700">Your Quote</label>
                  <input type="text" name="" id="" placeholder="Enter your quote" class="w-full px-4 py-3 rounded-lg bg-gray-200 mt-2 border focus:border-blue-500 focus:bg-white focus:outline-none" autofocus autocomplete v-model.trim="v$.form_data.quote.$model">
                  <div class="text-red-500" v-if="v$.form_data.quote.required.$invalid && show_error">
                    Quote is required
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
import { required } from '@vuelidate/validators'
import Swal from "sweetalert2";
export default {
  name: "CreateQuoteModal",
  setup: () => ({ v$: useVuelidate() }),
  data() {
    return {
      isOpen: false,
      show_error:false,
      form_data:{
        'quote':'',
      }
    };
  },

  computed: {
    isModalVisible() {
      return this.isOpen;
    }
  },

  methods: {
    async submit(e){
      e.preventDefault();
      if (this.checkSubmit()){
        this.isOpen = !this.isOpen;
        this.$toast.success("Successfully saved",{position:"top-right"});
        this.form_data.quote = '';
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
        await Swal.fire("Please write your quote", "", "info");
      }
    },
    checkSubmit(){
      this.v$.$touch()
      if (this.v$.form_data.quote.$invalid) {
        this.show_error = true;
        return false;
      }
      return true;
    },
    onToggle() {
      this.isOpen = !this.isOpen;
    },
  },
  validations: {
    form_data: {
      quote: {
        required,
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