<template>
    <div class="wrapper">
        <h1>Yizhaosan</h1>



        <Footer></Footer>
    </div>
</template>

<script>
    import Footer from "../components/Footer.vue";
    export default {
        name: "BusinessList",


        components: {
            Footer,
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
