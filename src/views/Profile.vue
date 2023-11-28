<template>
<div class="">
<!--  <EditProfileModal/>-->
  <div class="">
    <h1 class="" style="margin-top: 30px;margin-bottom: 30px;font-weight: bold;font-size: 18px">Account Information</h1>
    <table class="text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400" style="width: 400px">
      <tbody>
      <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
          Name
        </th>
        <td class="px-6 py-4" v-if="user != null">
          {{user[0].name}}
        </td>
      </tr>
      <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
          Email
        </th>
        <td class="px-6 py-4" v-if="user != null">
          {{user[0].email}}
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
import EditProfileModal from "../components/modals/EditProfileModal.vue";
export default {
  name: "Profile",
  components: {EditProfileModal},
  data(){
    return{
      user:null,
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
    }
  }
}
</script>

<style scoped>

</style>