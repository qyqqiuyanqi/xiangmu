<template>
  <div class="login">
    <el-card class="obox">
      <div class="logo">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <el-form ref="loginform" style="margin-top:15px" :model="Loginform" :rules="rules">
        <el-form-item prop="mobile">
          <el-input placeholder="请输入手机号" v-model="Loginform.mobile"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input placeholder="请输入验证码" style="width:230px" v-model="Loginform.code"></el-input>
          <el-button style="float:right">发送验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <el-checkbox v-model="Loginform.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" style="width:100%" @click="login">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {

  data () {
    let validator = function (rule, value, callback) {
      if (value) {
        callback()
      } else {
        callback(new Error('必须勾对'))
      }
    }
    return {
      Loginform: {
        mobiel: '',
        code: '',
        check: false
      },

      rules: {
        mobile: [
          {
            required: true,
            message: '手机号不能为空'
          },
          {
            pattern: /^1[3456789]\d{9}$/,
            message: '手机号格式不正确'
          }
        ],
        code: [
          { required: true, message: '验证码不能为空' },
          { pattern: /^\d{6}$/, message: '验证码不能为空' }
        ],
        check: [
          {
            validator
          }
        ]
      }
    }
  },
  methods: {
    login () {
      this.$refs.loginform.validate(isOk => {
        if (isOk) {
          this.$axios({
            url: '/authorizations',
            method: 'post',
            data: this.Loginform
          }).then(res => {
            // console.log(res.data.data.token);
            window.localStorage.setItem('user-token', res.data.token)
            this.$router.push('/')
          })
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login {
  height: 100vh;
  background: url("../../assets/img/login_bg.jpg");
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  .obox {
    width: 410px;
    height: 320px;
    .logo {
      text-align: center;
      img {
        height: 32px;
      }
    }
  }
}
</style>
