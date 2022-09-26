<template>
  <div class="login-container">
    <el-form
      ref="loginForm"
      :model="loginForm"
      :rules="loginFormRules"
      class="login-form"
      auto-complete="on"
      label-position="left"
    >
      <div class="title-container">
        <h3 class="title">
          <img src="../../assets/common/logo.png" class="login-logo" alt="">
        </h3>
      </div>
      <el-form-item prop="mobile" class="el-form-item__content">
        <i class="el-icon-mobile" style="margin-left:15px" />
        <el-input v-model="loginForm.mobile" style="width:90%; outline: 0;" />
      </el-form-item>

      <el-form-item prop="password" class="el-form-item__content">
        <i class="el-icon-lock" style="margin-left:15px" />
        <el-input v-model="loginForm.password" :type="passwprdType" style="width:83%;" />
        <span class="svg-container">
          <svg-icon icon-class="eye" />
        </span>
      </el-form-item>

      <el-form-item prop="verificationCode" class="el-form-item__content q">
        <i class="el-icon-discount" style="margin-left:15px" />
        <el-input v-model="loginForm.verificationCode" style="width:80%;" />
      </el-form-item>

      <el-button
        type="primary"
        style="width: 100%; height: 50px; margin-bottom: 30px; background-color: #4f69e7;"
      >登 录
      </el-button>
    </el-form>
  </div>
</template>

<script>
import { ValidPhone } from '@/utils/validate'
export default {
  data() {
    const phoneVaild = (rule, value, callback) => {
      if (!ValidPhone(value)) {
        callback(new Error('格式错误'))
      } else {
        callback()
      }
    }
    return {
      passwprdType: 'password',
      loginForm: {
        mobile: '18756426624',
        password: '123456',
        verificationCode: ''
      },
      loginFormRules: {
        mobile: [
          { required: true, message: '请输入手机号', trigger: 'blur' },
          { validator: phoneVaild, message: '手机格式错误', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 16, message: '密码格式不正确', trigger: 'blur' }
        ],
        verificationCode: { required: true, message: '请输入验证码', trigger: 'blur' }
      }
    }
  },
  watch: {},
  methods: {}
}
</script>

<style lang="scss">
$bg: #283443;
$light_gray: black;
$cursor: black;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container {
    position: relative;
    height: 100%;
    width: 100%;
    overflow: hidden;
    background-image: url(../../assets/common/background.png);
    background-repeat: no-repeat;
    background-size: cover;

    .login-form {
      position: absolute;
      width: 518px;
      height: 388px;
      top: 29%;
      padding: 76px 35px 0;
      background: #fff;
      -webkit-box-shadow: 0 3px 70px 0 rgb(30 111 72 / 35%);
      border-radius: 10px;
      .el-form-item__content{
        position: relative;
        border: 0.5px solid #f3f1f1;
        border-radius: 5px;
        line-height: 52px;
        font-size: 14px;
      }
      .q{
        width: 70%;
      }
      input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
    }
  }
}
</style>

<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;

  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 30px 35px 0;
    margin: 0 auto;
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
      .login-logo{
        position: absolute;
        width: 96px;
        height: 96px;
        top: -120px;
        left: 50%;
        margin-left: -48px;
        z-index:999;
      }
    }
  }

}
</style>
