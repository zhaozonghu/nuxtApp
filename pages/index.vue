<template>
  <section class="container">
      <app-swiper :banners="banners"></app-swiper>
      <!-- <nuxt-link v-show="isLogin" to="/login" tag="div" class="loginMask"></nuxt-link> -->
  </section>
</template>
<script>
  import axios from '~/plugins/axios'
  import AppSwiper from '~/components/AppSwiper.vue'
  import zbList from '~/components/home/zbList.vue'
  export default {
    async asyncData () {
        let { data } = await axios.get('/banner/')
        return {
          banners: data.banners
        }
    },
    components: {
      AppSwiper
    }
  }
</script>
<style>
.loginMask{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  right: 0;
  z-index: 9999999;
}
</style>
