<template>
  <div class="">
    <div class="mt-10 grid grid-cols-4 gap-4">
      <div class="flex items-center">
        <h1 class="text-4xl font-extrabold leading-none tracking-tight text-gray-900 md:text-5xl lg:text-6xl dark:text-white">Words to Live By</h1>
      </div>
      <div class="col-span-3">
        <div class="relative slide carousel_box">
          <div class="carousel-indicators absolute bottom-0 flex bg-white h-24 w-full justify-center items-center">
            <ol class="z-50 flex justify-start">
              <li v-for="(img, i) in images" :key="i"
                  class="md:w-3 md:h-3 bg-gray-300 rounded-full cursor-pointer mx-2"></li>
            </ol>
          </div>
          <div class="carousel-inner relative overflow-hidden carousel_box">
            <div v-for="(img, i) in images" :id="`slide-${i}`" :key="i"
                 :class="`${active === i ? 'active' : 'left-full'}`"
                 class="carousel-item inset-0 relative w-full transform transition-all duration-500 ease-in-out">
              <img class="block w-full" :src="img" alt="First slide" />
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>

<script>
// If you are using PurgeCSS, make sure to whitelist the carousel CSS classes
// import 'vue3-carousel/dist/carousel.css'
// import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'

export default {
  name: "HeroSlider",
  components: {

  },
  data(){
    return{
      images: [
        "https://picsum.photos/id/237/1024/800",
        "https://picsum.photos/id/238/1024/800",
        "https://picsum.photos/id/239/1024/800"
      ],
      active: 0
    }
  },
  mounted() {
    let i = 0;
    setInterval(() => {
      if (i > this.images.length - 1) {
        i = 0;
      }
      this.active = i;
      i++;
    }, 5000);
  }
}
</script>
<style scoped>
.left-full {
  left: -100%;
}

.carousel-item {
  float: left;
  position: relative;
  display: block;
  width: 100%;
  margin-right: -100%;
  backface-visibility: hidden;
}

.carousel-item.active {
  left: 0;
}
.carousel_box{
  height: 300px;
  width: 100%;
}
.carousel_item_box{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 55% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 55% 0, 79% 100%, 0% 100%);
  background-color: darkblue;
}
.right_image_box{
  height: 100%;
  background-color: darkred;
}
</style>