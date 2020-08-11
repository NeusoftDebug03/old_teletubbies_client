<template>
    <!-- 底部导航栏 -->
    <ul class="footer">
        <li @click="toIndex">
            <i class="fa fa-home"></i>
            <p>首页</p>
        </li>
        <li @click="toBusinessList">
            <i class="fa fa-compass"></i>
            <p>商品</p>
        </li>
        <li @click="toOrderList">
            <i class="fa fa-file-text-o"></i>
            <p>订单</p>
        </li>
        <li @click="toUserCenter">
            <i class="fa fa-user-o"></i>
            <p>我的</p>
        </li>
    </ul>
</template>

<script>
    export default {
        name: "FooterBar",
        methods: {
            toIndex() {
                this.$router.push("/index");
            },
            toBusinessList() {
                this.$router.push("/businessList")
            },
            toOrderList() {
                this.user = this.$getSessionStorage("user");
                if (this.user == null) {
                    this.$router.push("/login");
                } else {
                    this.$router.push("/orderList");
                }
            },
            toUserCenter() {
                this.user = this.$getSessionStorage("user");
                if (this.user == null) {
                    this.$router.push("/login");
                } else {
                    this.$router.push("/userCenter");
                }
            },
        },
    };
</script>

<style scoped>
    /****************** 底部菜单部分 ******************/
    .wrapper .footer {
        width: 100%;
        height: 14vw;
        border-top: solid 1px #ddd;
        background-color: #fff;

        position: fixed;
        left: 0;
        bottom: 0;

        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .wrapper .footer li {
        /*li本身的尺寸完全由内容撑起*/
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        color: #999;
        user-select: none;
        cursor: pointer;
    }
    .wrapper .footer li p {
        font-size: 2.8vw;
    }
    .wrapper .footer li i {
        font-size: 5vw;
    }
</style>
