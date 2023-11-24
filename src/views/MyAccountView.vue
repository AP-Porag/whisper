<template>
  <div class="" style="margin-top: 100px;padding-right: 78px;padding-left: 78px;">
    <div class="flex overflow-x-auto whitespace-nowrap mt-30">
      <button @click="$router.push('/my-account')" class="inline-flex items-center h-12 px-2 py-2 text-center text-gray-700 bg-transparent border border-b-0 border-gray-300 sm:px-4 dark:border-gray-500 -px-1 dark:text-white whitespace-nowrap cursor-base focus:outline-none hover:border-gray-400 dark:hover:border-gray-300">
        <span class="mx-1 text-sm sm:text-base">
            Quotes
        </span>
      </button>
      <button @click="$router.push('/my-account/profile')" class="inline-flex items-center h-12 px-2 py-2 text-center text-gray-700 border-gray-300 sm:px-4 dark:border-gray-500 rounded-t-md -px-1 dark:text-white whitespace-nowrap focus:outline-none">
        <span class="mx-1 text-sm sm:text-base">
            Profile
        </span>
      </button>
    </div>

    <div class="">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>

export default {
  name: "MyAccountView"
}
</script>

<style scoped>

</style>