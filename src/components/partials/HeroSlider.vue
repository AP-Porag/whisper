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
              <li v-for="(carousel, i) in carousels" :key="carousel.id"
                  class="md:w-3 md:h-3 bg-gray-300 rounded-full cursor-pointer mx-2"></li>
            </ol>
          </div>
          <div class="carousel-inner relative overflow-hidden carousel_box">
            <div v-for="(carousel, i) in carousels" :id="`slide-${i}`" :key="carousel.id"
                 :class="`${active === i ? 'active' : 'left-full'}`"
                 class="carousel-item inset-0 relative w-full transform transition-all duration-500 ease-in-out">
<!--              <img class="block w-full" :src="img" alt="First slide" />-->
              <div class="carousel_box_one relative">
                <div class="carousel_box_image" :style="{background:`url(${carousel.image })` + `no-repeat right  center/cover`}">
                  <div class="carousel_box_overlay"></div>
                </div>
                <div :class="`${carousel.class}`">
                  <div class="text_box p-10 text-right">
                    <h3 class="text-white text-3xl font-bold">{{carousel.quote}}</h3>
                    <h4 class="text-white text-2xl">- {{carousel.author}}</h4>
                  </div>
                </div>
              </div>
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
      carousels: [
        {
          id:1,
          quote:'When you have a dream, you\'ve got to grab it and never let go.',
          author:'Carol Burnett',
          image:'https://source.unsplash.com/silhouette-of-person-standing-on-rock-surrounded-by-body-of-water-odxB5oIG_iA',
          class:'carousel_box_polygon_background_1'
        },
        {
          id:2,
          quote:'Nothing is impossible. The word itself says \'I\'m possible!',
          author:'Audrey Hepburn',
          image:'https://source.unsplash.com/woman-sitting-around-table-holding-tablet-JBwcenOuRCg',
          class:'carousel_box_polygon_background_2'
        },
        {
          id:3,
          quote:'You are never too old to set another goal or to dream a new dream.',
          author:'Malala Yousafzai',
          image:'https://source.unsplash.com/man-standing-on-sand-while-spreading-arms-beside-calm-body-of-water-aK4iPNYipnU',
          class:'carousel_box_polygon_background_3'
        },
        {
          id:4,
          quote:'Spread love everywhere you go.',
          author:'Mother Teresa',
          image:'https://source.unsplash.com/closeup-photography-of-woman-smiling-mEZ3PoFGs_k',
          class:'carousel_box_polygon_background_4'
        },
        {
          id:5,
          quote:'There is nothing impossible to they who will try.',
          author:'Alexander the Great',
          image:'https://source.unsplash.com/a-person-standing-in-the-middle-of-a-road-Xokpz17GcDQ',
          class:'carousel_box_polygon_background_5'
        }
      ],
      active: 0
    }
  },
  mounted() {
    let i = 0;
    setInterval(() => {
      if (i > this.carousels.length - 1) {
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
.carousel_box_one{
  height: 300px;
  width: 100%;
  background: darkred;
}
.carousel_box_image{
  height: 100%;
  width: 600px;
  position: absolute;
  right: 0;
  top: 0;
}
.carousel_box_overlay{
  height: 100%;
  width: 100%;
  background-color: rgba(0,0,0,0.5);
}

.text_box{
  width: 65%;
}
.carousel_box_polygon_background_1{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,9,121,1) 79%, rgba(3,3,196,1) 100%);
}
.carousel_box_polygon_background_2{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  background: rgb(123,31,162);
  background: linear-gradient(90deg, rgba(123,31,162,1) 0%, rgba(142,36,170,1) 79%, rgba(171,71,188,1) 100%);
}
.carousel_box_polygon_background_3{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  background: rgb(1,71,55);
  background: linear-gradient(90deg, rgba(1,71,55,1) 0%, rgba(3,84,63,1) 79%, rgba(5,122,85,1) 100%);
}
.carousel_box_polygon_background_4{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  background: rgb(159,88,10);
  background: linear-gradient(90deg, rgba(159,88,10,1) 0%, rgba(194,120,3,1) 79%, rgba(250,202,21,1) 100%);
}
.carousel_box_polygon_background_5{
  height: 300px;
  width: 100%;
  clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  -webkit-clip-path: polygon(0 0, 65% 0, 79% 100%, 0% 100%);
  background: rgb(117,26,61);
  background: linear-gradient(90deg, rgba(117,26,61,1) 0%, rgba(153,21,75,1) 79%, rgba(214,31,105,1) 100%);
}
</style>