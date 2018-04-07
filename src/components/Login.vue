<template>
  <div>
    <div class="part">
      <vue-particles         
        color="#FFFF00"
        :particleOpacity="0.7"
        :particlesNumber="30"
        shapeType="circle"
        :particleSize="4"
        linesColor="#fff"
        :linesWidth="1"
        :lineLinked="true"
        :lineOpacity="0.5"
        :linesDistance="200"
        :moveSpeed="3"
        :hoverEffect="true"
        hoverMode="repulse"
        :clickEffect="true"
        clickMode="push">
      </vue-particles>
    </div>
    <el-form ref="AccountFrom" :model="account" :rules="rules" label-position="left" label-width="0px" class="demo-ruleForm login-container">
      <h3 class="title">管理员登录</h3>
      <el-form-item prop="username">
        <el-input type="text" v-model="account.username" auto-complete="off" placeholder="账号"></el-input>
      </el-form-item>
      <el-form-item prop="pwd">
        <el-input type="password" v-model="account.pwd" auto-complete="off" placeholder="密码"></el-input>
      </el-form-item>
      <!--<el-checkbox v-model="checked" checked class="remember">记住密码</el-checkbox>-->
      <el-form-item style="width:100%;">
        <el-button type="primary" style="width:100%;" @click.native.prevent="handleLogin" :loading="loading">登录</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  import API from "../api/api_user";

  export default {
    data() {
      return {
        loading: false,
        account: {
          username: "admin",
          pwd: "123456"
        },
        rules: {
          username: [{
              required: true,
              message: "请输入账号",
              trigger: "blur"
            }
            //{ validator: validaePass }
          ],
          pwd: [{
              required: true,
              message: "请输入密码",
              trigger: "blur"
            }
            //{ validator: validaePass2 }
          ]
        },
        checked: true
      };
    },
    methods: {
      handleLogin() {
        let that = this;
        this.$refs.AccountFrom.validate(valid => {
          if (valid) {
            this.loading = true;
            let loginParams = {
              username: this.account.username,
              pwd: this.account.pwd
            };
            API.login(loginParams)
              .then(
                function (result) {
                  that.loading = false;
                  if (result && result.id) {
                    localStorage.setItem("access-user", JSON.stringify(result));
                    //                that.$store.commit('SET_ROUTERS', user.permissions)
                    //                that.$router.addRoutes(that.$store.getters.addRouters);
                    //                that.$router.options.routes = that.$store.getters.routers;
                    that.$router.push({
                      path: "/"
                    });
                  } else {
                    that.$message.error({
                      showClose: true,
                      message: result.errmsg || "登录失败",
                      duration: 2000
                    });
                  }
                },
                function (err) {
                  that.loading = false;
                  that.$message.error({
                    showClose: true,
                    message: err.toString(),
                    duration: 2000
                  });
                }
              )
              .catch(function (error) {
                that.loading = false;
                console.log(error);
                that.$message.error({
                  showClose: true,
                  message: "请求出现异常",
                  duration: 2000
                });
              });
          }
        });
      }
    }
  };

</script>
<style>
  html {
    width: 100%;
    height: 100%;
  }
  html {
    background: url('../assets/images/login-bg.jpg') no-repeat;
    background-size: 100% 100%;
  }
  .part {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>

<style lang="scss" scoped>
  .login-container {
    /*box-shadow: 0 0px 8px 0 rgba(0, 0, 0, 0.06), 0 1px 0px 0 rgba(0, 0, 0, 0.02);*/
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin: 160px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;

    background: -ms-linear-gradient(top, #ace, #00c1de);
    /* IE 10 */
    background: -moz-linear-gradient(top, #ace, #00c1de);
    /*火狐*/
    background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#ace), to(#00c1de));
    /*谷歌*/
    background: -webkit-linear-gradient(top, #ace, #00c1de);
    /* Safari5.1 Chrome 10+ */
    background: -o-linear-gradient(top, #ace, #00c1de);
    /* Opera 11.10+ */
    .title {
      margin: 0px auto 40px auto;
      text-align: center;
      color: #505458;
    }
    .remember {
      margin: 0px 0px 35px 0px;
    }
  }

</style>
