<template>
  <section class="container">
      <!-- 轮播图 -->
      <app-swiper :banners="banners"></app-swiper>
      <!-- 游戏广告 -->
      <div class="home-game-show">
        <div class="home-notice-box">
          <div class="home-notice">
            <div class="home-broad-panel">
              <ul>
                <li v-for="(news,index) in gameNews" :key="index">
                <div v-if="news.type==1" class="home-notice-icon home-notice-icon1">公告</div>
                <div v-else class="home-notice-icon home-notice-icon2">获奖</div>
                <span class="home-broad-content home-broad-color1">{{news.nMsg}}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div class="other-boby-box">
        <div class="red-packed-box other-boby-child other-boby-child-left">
          <div class="other-boby-box-word">
            <h3>疯狂抢红包</h3>
            <p>
              免费红包任你拿
            </p>
          </div>
        </div>
        <div class="decrypt-box other-boby-child other-boby-child-right">
          <div class="other-boby-box-word">
            <h3>秘境解谜</h3>
            <p>
              益智数字趣味多
            </p>
          </div>
        </div>
    </div>
    <!-- 游戏列表 -->
    <div class="all-games-box">
      <span><i></i>全部游戏<i></i></span>
      <div class="home-game">
        <ul>
          <li v-for="(game,index) in gaems" :key="index">
              <div class="game-icon">
                <img  :src="game.cover">
              </div>
              <div class="game-title">
                <div class="game-name">{{game.name}}</div>
                <div class="game-des">{{game.des}}</div>
              </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- 领奖区 -->
    <div class="other-show reward-show">
      <div class="other-icon reward-icon">
      </div>
      <div class="other-show-text">
        <div class="other-show-title">
          <h3>领奖区 <span>超多奖品换不停</span></h3>
        </div>
        <div class="other-user-show">
          <ul>
            <li v-for="(news,index) in rewardNews" :key="index">
              <div class="h-reward-user-head">
                <img :src="news.head">
              </div>
              <div class="other-user-info">
                <span>{{news.name}}</span><span>{{news.goods}}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <nuxt-link to="/explore" tag="div" class="other-show-right"></nuxt-link>
    </div>
    <div class="h-qq-bg">
      <div class="h-qq-icon"></div>
      <div class="qq-text">
        QQ群:247024440 群内有福利!
      </div>
      <div class="h-qq-right"></div>
    </div>
  </section>
</template>
<script>
  import $ from 'jquery';
  import axios from '~/plugins/axios'
  import AppSwiper from '~/components/AppSwiper.vue'
  import zbList from '~/components/home/zbList.vue'

  export default {
    async asyncData () {
      let [banner,gameNews,gameList,rewardNews] = await Promise.all([
        axios.get('/banner/'),
        axios.get('/gameNews/'),
        axios.get('/gameList/'),
        axios.get('/RewardNews/')
      ])
       return {
        banners: banner.data.banners,
        gameNews:gameNews.data.rInfo,
        gaems: gameList.data.list,
        rewardNews:rewardNews.data.rInfo
      }
    },
    components: {
      AppSwiper
    },
    methods: {
          AutoScroll: function(ele,w) {
              ele.find("li").length > 1 && ele.find("ul:first").animate({
                  marginLeft: w
              }, 4500, "linear", function() {
                  $(this).css({
                      marginLeft: "0"
                  }).find("li:first").appendTo(this)
              })
          }
      },
      mounted(){
        var t=this;
        setInterval(function() {
            t.AutoScroll($(".home-broad-panel"),'-7.75rem')
        }, 2e3);
        setInterval(function() {
            t.AutoScroll($(".other-user-show"),'-6.16rem')
        }, 1e3);
      }
  }
</script>
<style>
.home-game-show {
    margin: 0 auto;
    height: 6.96rem;
    background: #1e2132;
    position: relative;
    display: table;
    height: auto
}
.home-notice-box {
    width: 10rem;
    height: .84rem;
    border-bottom: .013333rem solid #202a43
}

.home-notice-icon {
    z-index: 99;
    width: .853333rem;
    height: .4rem;
    border-radius: .24rem;
    color: #fff;
    margin-left: .4rem;
    text-align: center;
    line-height: .4rem;
    top: .226667rem
}

.home-notice,.home-notice-icon {
    font-size: .266667rem;
    position: absolute
}

.home-notice {
    width: 7.04rem;
    height: .466667rem;
    line-height: .466667rem;
    color: #686b7b
}
.home-broad-panel {
    width: 10rem;
    height: .8rem;
    background: #1e2132;
    overflow: hidden
}

.home-broad-panel ul {
    width: 100rem
}

.home-broad-panel li .home-broad-content {
    margin-left: 1.333333rem;
    width: 6.4rem;
    display: block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis
}

.home-broad-panel li {
    float: left;
    position: relative;
    height: .8rem;
    line-height: .8rem;
    font-size: .266667rem;
    color: #686b7b;
    overflow: hidden
}

.broad-panel li {
    clear: both
}

.home-notice-icon1 {
    background: #228fff
}

.home-notice-icon2 {
    background: #ff3556
}

.home-broad-color1 {
    color: #686b7b
}

.other-boby-box {
  height: 2.266667rem;
  padding: 0.133333rem 0.266667rem 0.266667rem;
}

.other-boby-box:after {
  content: ".";
  display: block;
  clear: both;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}
.other-boby-child {
  float: left;
  width: 4.613333rem;
  height: 1.800000rem;
}

.other-boby-child-right {
  float: right;
}

.other-boby-child-left {
  float: left;
}

.red-packed-box {
  background: url("../assets/images/index-red-pick.png") no-repeat center;
  background-size: 100% 100%;
}
.decrypt-box {
  background: url("../assets/images/index-decrypt-box.png") no-repeat center;
  background-size: 100%;
}
.other-boby-box-word {
  width: 2.466667rem;
  height: 0.880000rem;
  padding: 0.533333rem 0  0.360000rem;
  float: right;
}

.other-boby-box-word h3 {
  width: 100%;
  height: 0.426667rem;
  line-height: 0.426667rem;
  font-size: 0.426667rem;
  color: #fff;
  margin-bottom: 0.160000rem;
  font-weight: bold;
}

.other-boby-box-word p {
  width: 100%;
  height: 0.266667rem;
  font-size: 0.266667rem;
  color: #fff;
  opacity: 0.7;
}

.all-games-box {
  background: #1e2132;
}
.all-games-box:after {
  content: ".";
  display: block;
  clear: both;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.all-games-box span {
  display: block;
  text-align: center;
  height: 1.146667rem;
  line-height: 1.146667rem;
  font-size: 0.346667rem;
  color: #7f839b;
}

.all-games-box i {
  display: inline-block;
  height: 0.106667rem;
  width: 0.426667rem;
  border-top: 1px solid #fff;
  opacity: 0.2;
  margin: 0  0.133333rem;
}

.all-games-box li:after {
  content: ".";
  display: block;
  clear: both;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.all-games-box li {
  width: 3.333333rem;
  padding: 0.080000rem 0  0.426667rem;
  float: left;
  text-align: center;
}
.home-game a {
    text-decoration: none
}

.game-icon img,.home-game .game-icon {
    display: block;
    width: 1.333333rem;
    height: 1.333333rem;
    margin: 0 auto;
    background-size: cover
}

.game-name {
    height: .613333rem;
    line-height: .613333rem;
    color: #fff;
    font-weight: 100;
    font-size: .346667rem
}

.game-des {
    display: block;
    height: .293333rem;
    line-height: .293333rem;
    font-size: .293333rem;
    color: #7f839b
}
.reward-show {
    border-right: 1px solid #202a43
}
.other-show {
  margin-top: .266667rem;
  height: 2.133333rem;  
  background: #1e2132 url("../assets/images/show-little.png");
  background-size: cover;
  position: relative;
}

.other-show-right {
  display: block;
  width: 0.186667rem;
  height: 0.346667rem;
  position: absolute;
  top: 0.906667rem;
  right: 0.400000rem;
  background: url("../assets/images/index-right.png");
  background-size: cover;
}
.other-icon {
  float: left;
  width: 1.653333rem;
  height: 1.573333rem;
  margin: 0.226667rem 0 0 0.453333rem;
  background: url("../assets/images/home-reward-icon.png") no-repeat;
  background-size: cover;
}
.other-show-text {
    width: 7.6rem;
    margin-left: .2rem;
    float: right
}

.pk-show-text {
    margin-left: .133333rem
}

.other-show-title {
    margin: .426667rem 0 0 .106667rem
}

.other-show-title,.other-show-title h3 {
    font-size: .453333rem;
    line-height: .04rem;
    height: .453333rem;
    color: #fff
}

.other-show-title h3 span {
    height: .293333rem;
    font-size: .293333rem;
    padding-left: .32rem;
    color: #7f839b;
    font-weight: 100
}

.other-show-des {
    line-height: .56rem;
    height: .56rem;
    color: #7f839b;
    font-size: .32rem
}

.other-user-show {
    width: 6.16rem;
    height: .72rem;
    background: hsla(0,0%,100%,.1);
    border-radius: .72rem;
    overflow: hidden;
    margin-top: .24rem;
    position: relative
}

.other-user-show ul {
    width: 100rem;
    height: .72rem;
    position: absolute;
    overflow: hidden;
    left: 0
}

.other-user-info {
    width: 5.333333rem;
    display: inline-block;
    height: .72rem;
    line-height: .72rem;
    color: #fff;
    font-size: .293333rem;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap
}

.other-user-info,.qq-text {
    float: left;
    text-indent: .133333rem
}
.qq-text {
    margin-top: .24rem
}
.h-reward-user-head {
  margin: 0.066667rem;
  width: 0.586667rem;
  height: 0.586667rem;
  border-radius: 100%;
  float: left;
  background: url("../assets/images/head.png") top no-repeat;
  background-size: 100%;
  overflow: hidden;
}

.h-reward-user-head2 {
  float: right;
}

.h-reward-user-head img {
  display: block;
  width: 100%;
}
.h-qq-bg {
  margin: 0.133333rem auto 0.266667rem;
  padding-left: 0.746667rem;
  width: 6rem;
  height: 0.853333rem;
  font-size: 0.293333rem;
  color: #7d7d9b;
  text-align: center;
  background-size: 100%;
}

.h-qq-right {
  margin: 0.133333rem 0 0 0.066667rem;
  width: 0.680000rem;
  height: 0.466667rem;
  float: left;
  background: url("../assets/images/idnex-bottom-qq.png") no-repeat;
  background-size: cover;
}

.h-qq-icon {
  margin-top: 0.240000rem;
  float: left;
  width: 0.360000rem;
  height: 0.473333rem;
  background: url("../assets/images/qq.png") no-repeat center;
  background-size: 100%;
}
</style>
