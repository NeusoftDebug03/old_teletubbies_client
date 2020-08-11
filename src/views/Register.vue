<template>
    <div class="wrapper">
        <!-- header部分 -->
        <header>
            <div class="login-text">用户注册</div>
        </header>

        <!-- 表单部分 -->
        <ul class="form-box">
            <li>
                <div class="title">
                    手机号码：
                </div>
                <div class="content">
                    <input type="text" placeholder="手机号码" v-model="userId"/>
                </div>
            </li>
            <li>
                <div class="title">
                    密码：
                </div>
                <div class="content">
                    <input type="password" placeholder="密码" v-model="password"/>
                </div>
            </li>
            <li>
                <div class="title">
                    确认密码：
                </div>
                <div class="content">
                    <input type="password" placeholder="确认密码" v-model="checkpassword"/>
                </div>
            </li>
            <li>
                <div class="title">
                    用户名称:
                </div>
                <div class="content">
                    <input type="text" placeholder="用户名称" v-model="username">
                </div>
            </li>
            <li>
                <div class="title">
                    性别:
                </div>
                <div class="sex-choice">
                    <label><input type="radio" name="性别" value=1 checked v-model="usersex">男</label>
                    <label><input type="radio" name="性别" value=0 v-model="usersex">女</label>
                </div>
            </li>
        </ul>

        <div class="button-register">
            <button @click="register">注册</button>
        </div>
        <div class="button-go-back">
            <button @click="goback">返回</button>
        </div>


        <Footer></Footer>
    </div>
</template>

<script>
    import Footer from "../components/Footer.vue";

    export default {
        name: "register",
        data() {
            return {
                userId: "",
                password: "",
                checkpassword: "",
                username: "",
                usersex: "",
            };
        },
        methods: {
            register() {
                this.$router.push({path: "/register"});
                if (this.userId == "") {
                    alert("手机号不能为空");
                    return;
                }
                if (this.password == "") {
                    alert("密码不能为空");
                    return;
                }
                if (this.password != this.checkpassword) {
                    alert("两次密码输入不一致")
                }
                if (this.username == "") {
                    alert("用户名不能为空");
                    return;
                }
                if (this.usersex == "") {
                    alert("用户性别不能为空")
                    return;
                }

                this.$axios
                //用post提交必须要把数组转成字符串的格式才能提交，如果不转成字符串格式会序列化数据，提交过去的值为空值
                    .post(
                        "user/userIsExist",
                        {
                            userId: parseInt(this.userId),
                        }
                    )
                    .then((response) => {
                        // 控制台打印post返回结果
                        console.log(response.data);

                        if (response.data == 0) {
                            this.$axios
                                .post(
                                    "user/userLogin",
                                    {
                                        userId: this.userId,
                                        password: this.password,
                                        userName: this.username,
                                        userSex: this.usersex,
                                    }
                                )
                                .then((response) => {
                                    if (response.data == null) {
                                        alert("注册失败");
                                        return;
                                    } else {
                                        alert("注册成功")
                                        let user = response.data;
                                        //userImg数据量大，有可能溢出，不能放入SessionStorage中
                                        // user.userImg = "";
                                        this.$setSessionStorage("user", user);
                                        // this.$router.go(-1);
                                        this.$router.push({ path: "/index" })
                                    }
                                })
                                .catch((error) => {
                                    console.error(error);
                                });
                        }

                    })
                    .catch((error) => {
                        console.error(error);
                    })
            },
            goback() {
                this.$router.push({ path: "/index" });
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

    /****************** header ******************/
    .wrapper header {
        width: 100%;
        height: 12vw;
        background-color: #0097FF;

        display: flex;
        align-items: center;
        justify-content: center;
    }

    .wrapper header .login-text {
        font-size: 4.5vw;
        font-weight: bolder;
        color: #fff;
        margin: 0 auto;
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

    .wrapper .form-box li .sex-choice {
        flex: 2;
    }

    .wrapper .form-box li .sex-choice label {
        letter-spacing: 10px;
    }

    .wrapper .form-box li .sex-choice label, input {
        margin: 0 auto;
        vertical-align: middle;
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
        color: white;
        background-color: #38ca73;
        border-radius: 5px;
        border: none;
        outline: none;
    }

    .wrapper .button-go-back {
        width: 100%;
        box-sizing: border-box;
        padding: 5vw 3vw 0 3vw;
    }

    .wrapper .button-go-back button {
        width: 100%;
        height: 12vw;
        font-size: 6vw;
        font-weight: 700;
        color: #666666;
        background-color: #eeeeee;
        border-radius: 5px;
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
