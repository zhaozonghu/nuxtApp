<template>
    <div class="wap-login-bg">
        <nuxt-link to="/" tag="div" class="wap-login-bg-cancel">取消</nuxt-link>
        <div class="wap-login-content">
            <form ref="loginForm" :model="form">
                <div class="wap-login-telbox">
                    <div class="wap-login-phone-icon"></div> 
                    <input type="number" v-model="form.userName" class="login-tel" maxlength="11" placeholder="请输入手机号">
                </div>
                <div class="wap-login-codebox wap-login-codebox-password">
                    <div class="wap-login-msg-icon"></div> 
                    <input type="password" v-model="form.password" class="login-code" maxlength="20" placeholder="请输入密码">
                </div>
                <div class="wap-login-btn" @click="handleSubmit"> 登录 </div>
                <div class="wap-login-box-bottom-butten">
                    <div class="wap-login-box-bottom-butten-left">免费注册</div>
                    <div class="wap-login-box-bottom-butten-right">忘记密码</div>
                </div>
            </form>
        </div>
        <div class="popup normal-box-popup"> 
            <div class="wap-login-error-bg"> 
                <div class="login-error-icon">!</div> <div class="login-error-tips">{{form.message}}</div> 
            </div> 
        </div>
    </div>
</template>

<script>
import $ from 'jquery';
export default {
  data() {
    return {
      form: {
        userName: "15883968623",
        password: "",
        message:""
      }
    };
  },
  methods: {
    handleSubmit() {
        var reg = /^1[3|4|5|7|8][0-9]{9}$/;
        if (this.form.userName == "") {
            this.form.message="手机号码不能为空";
            this.showPop();
            return false;
        }else if(!reg.test(this.form.userName)){
            this.form.message="手机号码格式错误";
            this.showPop();
            return false;
        }
        if (this.form.password == "") {
            this.form.message="密码不能为空";
            this.showPop();
            return false;
        }
        if(this.form.userName != ""&&this.form.password != ""){
            this.$store.state.isLogin=1;
            this.$router.go(-1);
        }
    },
    showPop(){
        $('.popup').fadeIn(function(){
            setTimeout(function(){
                $('.popup').fadeOut();
            },800)
        });
    }
  },
  mounted(){
  }
};
</script>

<style scoped>
.wap-login-box {
  width: 10rem;
  margin: 0 auto;
  position: absolute;
  top: 0;
  bottom: 0;
}

.wap-login-bg {
  position: absolute;
  z-index: 9999;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
      max-width: 10rem;
    margin: 0 auto;
  padding: 0.4rem 0.48rem 1.333333rem;
  background: url("../assets/images/login-bg.png") no-repeat center top;
  background-size: 2.16rem 2.746667rem;
  background-position-y: 1.173333rem;
  background-color: #1e2132;
}
.wap-login-content {
  width: 8.666667rem;
  min-height: 6.373333rem;
  padding: 0 0.666667rem;
  position: absolute;
  left: 0;
  top: 4.5rem;
}
.wap-login-codebox,
.wap-login-telbox {
  position: relative;
  margin: 0 auto;
  height: 1.6rem;
  width: 8.666667rem;
  border-bottom: 0.013333rem solid #263354;
}
.wap-login-phone-icon {
  position: absolute;
  top: 0.56rem;
  width: 0.4rem;
  height: 0.426667rem;
  background: url("../assets/images/login-phone.png") no-repeat;
  background-size: 100%;
}
.wap-login-msg-icon {
  position: absolute;
  top: 0.613333rem;
  width: 0.4rem;
  height: 0.426667rem;
  background: url("../assets/images/wap-login-codebox-password.png") no-repeat;
  background-size: 100%;
}
.login-tel {
  font-size: 0.4rem;
}

.login-code,
.login-tel {
  position: absolute;
  top: 0.133333rem;
  left: 0.8rem;
  width: 6rem;
  height: 1.333333rem;
  line-height: 1.333333rem;
  background: #1e2132;
  color: #fff;
  border: 0;
  outline: 0;
}

.login-code {
  font-size: 0.373333rem;
}

input::-moz-placeholder {
  color: #4c4c61;
}

input:-ms-input-placeholder {
  color: #4c4c61;
}

input::-webkit-input-placeholder {
  color: #4c4c61;
}
.wap-login-btn {
  width: 8.666667rem;
  height: 1.2rem;
  border-radius: 0.613333rem;
  background: #ff3556;
  color: #fff;
  text-align: center;
  line-height: 1.2rem;
  font-size: 0.453333rem;
  margin-top: 0.826667rem;
}
.wap-login-box-bottom-butten {
  width: 4.866667rem;
  height: 0.533333rem;
  line-height: 0.48rem;
  font-size: 0.333333rem;
  color: #7d7d9b;
  margin: 0.453333rem auto;
}

.wap-login-box-bottom-butten-left {
  width: 2.413333rem;
  border-right: 0.013333rem solid #34374f;
  height: 100%;
  text-align: center;
  float: left;
}

.wap-login-box-bottom-butten-right {
  width: auto;
  padding-left: 0.533333rem;
  float: left;
}

.wap-login-bg-cancel {
  font-size: 0.36rem;
  color: #fff;
}

.popup {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    z-index: 99;
    display: none;
    background: rgba(0, 0, 0, .6);
}

.popup-top {
    top: 0;
    right: auto;
    bottom: auto;
    left: 50%;
    -webkit-transform: translate3d(-50%,0,0);
    transform: translate3d(-50%,0,0)
}

.popup-right {
    top: 50%;
    right: 0;
    bottom: auto;
    left: auto;
    -webkit-transform: translate3d(0,-50%,0);
    transform: translate3d(0,-50%,0)
}

.popup-bottom {
    top: auto;
    right: auto;
    bottom: 0;
    left: 50%;
    -webkit-transform: translate3d(-50%,0,0);
    transform: translate3d(-50%,0,0)
}

.popup-left {
    top: 50%;
    right: auto;
    bottom: auto;
    left: 0;
    -webkit-transform: translate3d(0,-50%,0);
    transform: translate3d(0,-50%,0)
}

.popup-slide-bottom-transition,.popup-slide-left-transition,.popup-slide-right-transition,.popup-slide-top-transition {
    -webkit-transition: -webkit-transform .15s ease;
    transition: -webkit-transform .15s ease;
    transition: transform .15s ease;
    transition: transform .15s ease,-webkit-transform .15s ease
}

.popup-slide-top-enter,.popup-slide-top-leave {
    -webkit-transform: translate3d(-50%,-100%,0);
    transform: translate3d(-50%,-100%,0)
}

.popup-slide-right-enter,.popup-slide-right-leave {
    -webkit-transform: translate3d(100%,-50%,0);
    transform: translate3d(100%,-50%,0)
}

.popup-slide-bottom-enter,.popup-slide-bottom-leave {
    -webkit-transform: translate3d(-50%,100%,0);
    transform: translate3d(-50%,100%,0)
}

.popup-slide-left-enter,.popup-slide-left-leave {
    -webkit-transform: translate3d(-100%,-50%,0);
    transform: translate3d(-100%,-50%,0)
}

.popup-fade-transition {
    -webkit-transition: opacity .15s;
    transition: opacity .15s
}

.popup-fade-enter,.popup-fade-leave {
    opacity: 0
}
.wap-login-error-bg {
    width: 5.066667rem;
    height: 2.533333rem;
    border-radius: .293333rem;
    background: rgba(255,255,255,.9);
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate3d(-50%,-50%,0);
    transform: translate3d(-50%,-50%,0);
}

.login-error-icon {
    width: .773333rem;
    height: .773333rem;
    border: .04rem solid #ff4a4a;
    border-radius: 100%;
    position: absolute;
    top: .4rem;
    left: 2.133333rem;
    font-size: .48rem;
    color: #ff4a4a;
    text-align: center;
    line-height: .773333rem;
    font-weight: 700
}

.login-error-tips {
    color: #1b223c;
    font-size: .4rem;
    position: absolute;
    width: 4rem;
    text-align: center;
    top: 1.6rem;
    left: .533333rem
}

</style>