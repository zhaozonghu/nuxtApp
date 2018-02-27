<template>
  <div class="my-swiper" v-swiper:mySwiper="swiperOption">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="(banner,index) in banners" :key="index">
          <nuxt-link :to="banner.link" tag="a">
          <img :src="banner.img">
          </nuxt-link>
      </div>
    </div>
    <div class="swiper-pagination swiper-pagination-bullets"></div>
  </div>
</template>

<script>
  export default {
      props: ['banners'],
    data () {
      return {
        swiperOption: {
          loop: true,
          slidesPerView: 'auto',
          centeredSlides: true,
          spaceBetween: 30,
          autoplay: {
            delay: 5000,
            disableOnInteraction: false
          },
          pagination: {
            el: '.swiper-pagination',
            dynamicBullets: true
          },
          on: {
            slideChange() {},
            tap() {}
          }
        }
      }
    },
    mounted() {
    }
  }
</script>


<style scoped>
.my-swiper {
    position: relative;
    height: 3.493333rem;
    width: 100%;
}
.swiper-slide {
    text-align: center;
    font-size: 38px;
    font-weight: 700;
    background-color: #eee;
    display: flex;
    justify-content: center;
    align-items: center;
}
.swiper-slide img{
    width: 100%;
    display: block;
}

.swiper-pagination  .swiper-pagination-bullet {
    background-color: red;
}
</style>