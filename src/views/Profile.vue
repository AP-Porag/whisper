<template>
<div class="">
  <EditProfileModal/>
  <div class="">
    <h1 class="" style="margin-top: 30px;margin-bottom: 30px;font-weight: bold;font-size: 18px">Account Information</h1>
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
      <tbody>
      <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
          Name
        </th>
        <td class="px-6 py-4">
          {{user.name}}
        </td>
      </tr>
      <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
          Email
        </th>
        <td class="px-6 py-4">
          {{user.email}}
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
      user:[],
    }
  },
  methods:{

  }
}
</script>

<style scoped>

</style>