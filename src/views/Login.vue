<template>
    <div class="wrapper">
        <!-- header部分 -->
        <header>
            <p>用户登陆</p>
        </header>

        <!-- 表单部分 -->
        <ul class="form-box">
            <li>
                <div class="title">
                    手机号码：
                </div>
                <div class="content">
                    <input type="text" placeholder="手机号码" v-model="userId" />
                </div>
            </li>
            <li>
                <div class="title">
                    密码：
                </div>
                <div class="content">
                    <input type="password" placeholder="密码" v-model="password" />
                </div>
            </li>
        </ul>

        <div class="button-login">
            <button @click="login">登陆</button>
        </div>
        <div class="button-register">
            <button @click="register">去注册</button>
        </div>

        <Footer></Footer>
    </div>
</template>

<script>
    import Footer from "../components/Footer.vue";
    export default {
        name: "Login",
        data() {
            return {
                userId: "",
                password: "",
            };
        },
        methods: {
            register() {
                this.$router.push({ path: "/register" });
            },
            login() {
                if (this.userId == "") {
                    alert("手机号码不能为空！");
                    return;
                }
                if (this.password == "") {
                    alert("密码不能为空！");
                    return;
                }
                //用post提交必须要把数组转成字符串的格式才能提交，如果不转成字符串格式会序列化数据，提交过去的值为空值
                this.$axios
                    .post(
                        "user/userLogin",
                        {
                            // this.$querystring({
                            userId: this.userId,
                            password: this.password,
                            // }),
                        }

                    )
                    .then((response) => {

                        // 控制台打印response.data
                        console.log("response.data: " + response);

                        if (response.data == null) {
                            alert("用户名或密码不正确");
                        } else {
                            let user = response.data;
                            //userImg数据量大，有可能溢出，不能放入SessionStorage中
                            // user.userImg = "";
                            this.$setSessionStorage("user", user);
                            // this.$router.go(-1);
                        }
                    })
                    .catch((error) => {
                        console.error(error);
                    });
            },
        },
        components: {
            Footer,
        },
    };
</script>

<style scoped>
    /****************** 总容器 ******************/
    .wrapper {
        width: 100%;
        height: 100%;
    }

    /****************** header部分 ******************/
    .wrapper header {
        width: 100%;
        height: 12vw;
        background-color: #0097ff;
        color: #fff;
        font-size: 4.8vw;

        position: fixed;
        left: 0;
        top: 0;
        z-index: 1000;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    /****************** 表单部分 ******************/
    .wrapper .form-box {
        width: 100%;
        /*margin: 10vw 3vw 0 3vw;*/
        margin-top: 8vw;
    }

    .wrapper .form-box li {
        display: flex;
        align-content: center;
        padding: 5vw 3vw 0 3vw;
        box-sizing: border-box;
    }

    .wrapper .form-box li .title {
        flex: 1;
        font-size: 5vw;
        font-weight: 700;
        color: #686869;
    }

    .wrapper .form-box li .content {
        flex: 2;
    }

    .wrapper .form-box li .content input {
        border: none;
        outline: none;
        width: 100%;
        height: 6vw;
        font-size: 5vw;
    }

    .wrapper .button-login {
        width: 100%;
        box-sizing: border-box;
        padding: 5vw 3vw 0 3vw;
    }
    .wrapper .button-login button {
        width: 100%;
        height: 12vw;
        font-size: 6vw;
        font-weight: 700;
        color: #fff;
        background-color: #38ca73;
        border-radius: 4px;

        border: none;
        outline: none;
    }
    .wrapper .button-register {
        width: 100%;
        box-sizing: border-box;
        padding: 5vw 3vw 0 3vw;
    }
    .wrapper .button-register button {
        width: 100%;
        height: 12vw;
        font-size: 6vw;
        font-weight: 700;
        /*与上面登陆按钮不同的只有颜色、背景色、边框不同*/
        color: #666;
        background-color: #eee;
        border: solid 1px #ddd;
        border-radius: 4px;

        border: none;
        outline: none;
    }
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
