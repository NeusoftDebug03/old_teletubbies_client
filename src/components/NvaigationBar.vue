<template>
    <!-- 顶部导航栏 -->
    <div>
        <div class="site-nav-bg">
            <div class="site-nav w1200">
                <p class="sn-back-home">
                    <i class="layui-icon layui-icon-home"></i>
                    <a @click="toIndex">首页</a>
                </p>
                <div class="sn-quick-menu">
                    <div class="login">
                        <a @click="toLogin">登陆</a>
                    </div>
                    <div class="sp-cart">
                        <a @click="toShopcart">购物车</a>
                        <span>2</span>
                    </div>
                </div>
            </div>
        </div>
        <div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "NvaigationBar",
        methods: {
            toIndex() {
                this.$router.push("/index");
            },
            toLogin() {
                this.user = this.$getSessionStorage("user");
                if (this.user == null) {
                    this.$touter.push("/login");
                } else {
                    this.$router.push("/userCenter");
                }
            },
            toShopcart() {
                this.user = this.$getSessionStorage("user");
                if (this.user == null) {
                    this.$router.push("/login");
                } else {
                    this.$router.push("/shopcart");
                }
            },
        },
    };
</script>

<style scoped>

</style>