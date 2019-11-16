<template>
    <div class="login">
        <!-- elementUI -->
        <el-card class="login-card">
            <!-- 卡片内容  -->
  <div class="title">
<img src="../../assets/img/logo_index.png" alt="">
  </div>
  <!-- 表单 -->
  <el-form
  style="margin-top:30px"
  :model="loginForm"
  :rules="loginRules"
  ref="formLog"
  >
      <!-- 表单域 -->
      <el-form-item prop="mobile">
          <!-- 手机号 -->
<el-input v-model="loginForm.mobile" placeholder="请输入手机号"></el-input>
      </el-form-item>

      <el-form-item prop="code">
          <!-- 验证码 -->
          <el-input style="width:280px" v-model="loginForm.code"  placeholder="请输入验证码"></el-input>
          <el-button style="float:right">发送验证码</el-button>
      </el-form-item>

      <el-form-item prop="checked">
          <!-- 勾选框 -->
          <el-checkbox v-model="loginForm.checked">我已阅读并同意用户协议及条款</el-checkbox>
      </el-form-item>

      <el-form-item>
          <!-- 登录按钮 -->
          <el-button style="width:100%" type="primary" @click="login">登录</el-button>
      </el-form-item>
  </el-form>
</el-card>
    </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        mobile: '',
        code: '',
        checked: false
      },
      loginRules: {
        mobile: [{ required: true, message: '请输入您的手机号' },
          { pattern: /^1[3456789]\d{9}$/, message: '请输入合法的手机号' }],
        code: [{ required: true, message: '请输入您的验证码' },
          { pattern: /^\d{6}$/, message: '验证码为6位数字' }],
        checked: [{ validator: function (rule, value, callback) {
          if (value) {
            callback()
          } else {
            callback(new Error('您需要勾选协议'))
          }
        } }]
      }
    }
  },
  methods: {
    login () {
      this.$refs.formLog.validate(function (isOK) {
        if (isOK) {
          console.log('校验成功')
        }
      })
    }
  }
}
</script>

<style lang='less' scoped>
.login{
    background-image: url('../../assets/img/login_bg.jpg');
    background-size: cover;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    .login-card {
        width: 440px;
        height: 360px;
        .title {
            text-align: center;
            img {
                height: 45px;
            }
        }
    }
}
</style>
