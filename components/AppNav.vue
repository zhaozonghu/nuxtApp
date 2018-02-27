<template>
        <nav class="bar bar-tab">
            <nuxt-link to="/" tag="div" class="tab-item" exact>
                <div class="home-icon home-icon-g"></div> <span class="tab-label">游戏</span>
                <div class="redDot" v-show="$store.state.newMsgCount"></div>
            </nuxt-link>
            <nuxt-link to="/contact" tag="div" class="tab-item" exact>
                <div class="home-icon home-icon-w"></div> <span class="tab-label">福利</span>
                <div class="redDot" style="display: none;"></div>
            </nuxt-link>
            <nuxt-link to="/explore" tag="div" class="tab-item" exact>
                <div class="home-icon home-icon-r"></div> <span class="tab-label">奖励</span>
            </nuxt-link>
            <nuxt-link v-if="$store.state.isLogin" to="/self" tag="div" class="tab-item" exact>
                <div class="home-icon home-icon-m"></div> <span class="tab-label">我的</span>
                <div class="redDot" style="display: none;"></div>
            </nuxt-link>
            <nuxt-link v-else to="/login" tag="div" class="tab-item" exact>
                <div class="home-icon home-icon-m"></div> <span class="tab-label">我的</span>
                <div class="redDot" style="display: none;"></div>
            </nuxt-link>
        </nav>
</template>

<script>
    export default {
        props: ['isLogin']
    }
</script>

<style scoped>
.bar-tab {
    width: 10.000000rem;
    height: 1.406667rem;
    color: #7f839b;
    background: #151723;
    font-size: .266667rem;
    position: fixed;
    z-index: 999;
    left: auto;
    right:auto;
    bottom: 0;
}

.tab-item {
    position: relative;
    width: 2.493333rem;
    text-align: center;
    float: left;
    color: #7f839b;
    margin-top: .2rem
}

.bar-tab .active-link {
    color: #ff3556
}

.home-icon {
    width: 0.640000rem;
    height: 0.533333rem;
    margin: 0 auto 0.133333rem;
}

.home-icon-g {
    background: url("../assets/images/nav/home-icon-g.png") no-repeat center;
    background-size: 0.640000rem 0.533333rem;
}

.active-link .home-icon-g {
    background: url("../assets/images/nav/home-icon-g-h.png") no-repeat center;
    background-size: 0.640000rem 0.533333rem;
}

.home-icon-w {
    background: url("../assets/images/nav/home-icon-w.png") no-repeat center;
    background-size: 0.586667rem 0.506667rem;
}

.active-link .home-icon-w {
    background: url("../assets/images/nav/home-icon-w-h.png") no-repeat center;
    background-size: 0.586667rem 0.506667rem;
}

.home-icon-m {
    background: url("../assets/images/nav/home-icon-m.png") no-repeat center;
    background-size: 0.426667rem 0.533333rem;
}

.active-link .home-icon-m {
    background: url("../assets/images/nav/home-icon-m-h.png") no-repeat center;
    background-size: 0.426667rem 0.533333rem;
}

.home-icon-r {
    background: url("../assets/images/nav/home-icon-r.png") no-repeat center;
    background-size: 0.533333rem 0.506667rem;
}

.active-link .home-icon-r {
    background: url("../assets/images/nav/home-icon-r-h.png") no-repeat center;
    background-size: 0.533333rem 0.506667rem;
}

.redDot {
    width: .213333rem;
    height: .213333rem;
    border-radius: 100%;
    background: #ff3645;
    position: absolute;
    top: .133333rem;
    right: .533333rem
}
</style>