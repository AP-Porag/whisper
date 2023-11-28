<template>
<div class="">
  <div class="" style="margin-top: 100px;">
    <div class="m-auto grid grid-cols-1 md:grid-cols-2 gap-20" v-if="items.length > 0">
      <div class="blog_post" v-for="(item,index) in items" :key="item.id">
        <div class="img_pod">
          <img src="https://pbs.twimg.com/profile_images/890901007387025408/oztASP4n.jpg" alt="random image">
        </div>
        <div class="container_copy">
          <h3 class="created_at">{{item.created_at}}</h3>
          <p>{{item.quote}}</p>
          <div class="flex justify-content-between">
            <input type="text" v-model.trim="v$.form_data.quote.$model" name="" id="" placeholder="Enter your quote to edit" class="w-full px-4 py-3 rounded-lg bg-gray-200 mt-2 border focus:border-blue-500 focus:bg-white focus:outline-none">
            <button @click.prevent="update(item.id)" data-toggle="modal" data-target="#myModal" type="button" style="padding: 9px;margin: 8px;" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center me-2 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800 dark:hover:bg-blue-500">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
              </svg>
              <span class="sr-only">Edit</span>
            </button>
          </div>
          <div class="text-red-500" v-if="v$.form_data.quote.required.$invalid && show_error">
            Quote is required
          </div>
          <h1>"{{item.user_name}}</h1>
          <div class="button_div" style="margin-bottom: 30px">
            <button @click="like(item.id)" type="button" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center me-2 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800 dark:hover:bg-blue-500">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6.633 10.5c.806 0 1.533-.446 2.031-1.08a9.041 9.041 0 012.861-2.4c.723-.384 1.35-.956 1.653-1.715a4.498 4.498 0 00.322-1.672V3a.75.75 0 01.75-.75A2.25 2.25 0 0116.5 4.5c0 1.152-.26 2.243-.723 3.218-.266.558.107 1.282.725 1.282h3.126c1.026 0 1.945.694 2.054 1.715.045.422.068.85.068 1.285a11.95 11.95 0 01-2.649 7.521c-.388.482-.987.729-1.605.729H13.48c-.483 0-.964-.078-1.423-.23l-3.114-1.04a4.501 4.501 0 00-1.423-.23H5.904M14.25 9h2.25M5.904 18.75c.083.205.173.405.27.602.197.4-.078.898-.523.898h-.908c-.889 0-1.713-.518-1.972-1.368a12 12 0 01-.521-3.507c0-1.553.295-3.036.831-4.398C3.387 10.203 4.167 9.75 5 9.75h1.053c.472 0 .745.556.5.96a8.958 8.958 0 00-1.302 4.665c0 1.194.232 2.333.654 3.375z" />
              </svg>
              <span class="ml-2">  | {{item.like}}</span>
            </button>
            <button @click="dislike(item.id)" type="button" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center me-2 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800 dark:hover:bg-blue-500">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M7.5 15h2.25m8.024-9.75c.011.05.028.1.052.148.591 1.2.924 2.55.924 3.977a8.96 8.96 0 01-.999 4.125m.023-8.25c-.076-.365.183-.75.575-.75h.908c.889 0 1.713.518 1.972 1.368.339 1.11.521 2.287.521 3.507 0 1.553-.295 3.036-.831 4.398C20.613 14.547 19.833 15 19 15h-1.053c-.472 0-.745-.556-.5-.96a8.95 8.95 0 00.303-.54m.023-8.25H16.48a4.5 4.5 0 01-1.423-.23l-3.114-1.04a4.5 4.5 0 00-1.423-.23H6.504c-.618 0-1.217.247-1.605.729A11.95 11.95 0 002.25 12c0 .434.023.863.068 1.285C2.427 14.306 3.346 15 4.372 15h3.126c.618 0 .991.724.725 1.282A7.471 7.471 0 007.5 19.5a2.25 2.25 0 002.25 2.25.75.75 0 00.75-.75v-.633c0-.573.11-1.14.322-1.672.304-.76.93-1.33 1.653-1.715a9.04 9.04 0 002.86-2.4c.498-.634 1.226-1.08 2.032-1.08h.384" />
              </svg>
              <span class="ml-2">  | {{item.dislike}}</span>
            </button>
            <button @click="favorite(item.id)" type="button" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center me-2 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800 dark:hover:bg-blue-500">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z" />
              </svg>
              <span class="ml-2"> | {{item.favorite}}</span>
            </button>
            <button @click="deleteQuote(index,item.id)" v-if="user != null && author" type="button" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center me-2 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800 dark:hover:bg-blue-500">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
              </svg>
              <span class="sr-only">Delete</span>
            </button>
          </div>
        </div>
      </div>
    </div>
    <p v-else class="text-orange-500">You dont create any quote till now, Please make a quote</p>
  </div>
</div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
import EditQuoteModal from "../components/modals/EditQuoteModal.vue";
import {required} from "@vuelidate/validators";
import {useVuelidate} from "@vuelidate/core";

export default {
  name: "MyQuote",
  components: {EditQuoteModal},
  setup: () => ({ v$: useVuelidate() }),
  data(){
    return{
      user:null,
      author:true,
      dontShowQuoteBox:true,
      items:[],
      show_error:false,
      form_data:{
        quote:'',
      }
    }
  },
  created() {
    this.getLocalUser();
    this.getAllQuotes();
  },
  methods:{
    async getAllQuotes(){
      let self = this;
      console.log('user : '+this.user)
      console.log(this.user[0].id)
      await axios
          .get(`https://whisper.shadeofattire.com/api/quotes/user/quotet/${this.user[0].id}`)
          .then(function (response) {

            if (response.data.status == 200){
              self.items = response.data.data
            }
          })
          .catch(function (err) {
            console.log(err)

          });
    },
    async like(id){
      let self = this;5
      await axios
          .post(`https://whisper.shadeofattire.com/api/quotes/increase/like/${id}`)
          .then(function (response) {

            if (response.data.status == 200){
              var food = self.items.find(item => item.id === id)

              let increase = food.like != null? parseInt(food.like)+1 : 0 +1;
              food.like = increase
              self.$toast.success('Saved',{position:"top-right"})

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
    },
    async dislike(id){
      let self = this;5
      await axios
          .post(`https://whisper.shadeofattire.com/api/quotes/increase/dislike/${id}`)
          .then(function (response) {

            if (response.data.status == 200){
              var food = self.items.find(item => item.id === id)

              let increase = food.dislike != null? parseInt(food.dislike)+1 : 0+1;
              food.dislike = increase
              self.$toast.success('Saved',{position:"top-right"})

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
    },
    async favorite(id){
      let self = this;5
      await axios
          .post(`https://whisper.shadeofattire.com/api/quotes/increase/favorite/${id}`)
          .then(function (response) {

            if (response.data.status == 200){
              var food =  self.items.find(item => item.id === id)

              let increase = food.like != null? parseInt(food.favorite)+1 : 0+1;
              food.favorite = increase
              self.$toast.success('Saved',{position:"top-right"})

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
    },
    async deleteQuote(index,id){
      let self = this;
      await axios
          .delete(`https://whisper.shadeofattire.com/api/quotes/${id}`)
          .then(function (response) {

            if (response.data.status == 200){
              self.items.splice(index, 1);
              // var food = self.items.find(item => item.id === id)
              //
              // let increase = parseInt(food.favorite)+1;
              // food.favorite = increase
              self.$toast.success('Saved',{position:"top-right"})

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
    },
    async getLocalUser(){
      let user = JSON.parse(localStorage.getItem('user')) || null;
      console.log(user)

      if (user == 'undefined'){
        console.log('undefineds')
      }else {
        this.user = user;
      }
    },
    async update(id){
      let self = this;
      if (this.checkSubmit()){
        // Submit form
        await axios
            .put(`https://whisper.shadeofattire.com/api/quotes/${id}`, self.form_data)
            .then(function (response) {
              console.log(response.data.status)
              if (response.data.status == 200){
                self.$toast.success("Successfully updated",{position:"top-right"});
                self.form_data.quote = '';
                window.location.reload()
              }

            })
            .catch(function (err) {
              try {
                Swal.fire("Something went wrong", "", "error");
              } catch (e) {
                Swal.fire("Something went wrong", "", "error");
              }
            });
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
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,700&display=swap");
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

.blog_post {
  background: #fff;
  border-radius: 10px;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  position: relative;
}


.container_copy {
//padding: 6rem 4rem 0px 4rem;
  padding: 30px 30px 0px 30px;
}

.img_pod {
  height: 60px;
  width: 60px;
  background: linear-gradient(90deg, #ff9966, #ff5e62);
  z-index: 10;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  border-radius: 100%;
  position: absolute;
  left: -4%;
  top: -10%;
  display: flex;
  align-items: center;
  justify-content: center;
}

img {
  height: 60px;
  width: 60px;
  position: relative;
  border-radius: 100%;
  box-shadow: 1px 1px 2rem rgba(0, 0, 0, 0.3);
  z-index: 1;
}

.created_at {
  margin: 0 0 0.5rem 0;
  color: #999;
  font-size: 14px;
}

h1 {
  margin: 0 0 15px 0;
  font-size: 14px;
  letter-spacing: 0.5px;
  color: #999;
  text-align: right;
}

p {
  margin: 0 0 15px 0;
  font-size: 16px;
  line-height: 1.5rem;
  color: #333;
}

</style>