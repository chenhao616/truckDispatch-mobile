<template>
  <div class="content">
    <div class="login-bg"></div>
    <h1 class="system-title">
      鞍钢矿业
      <br />智能工厂浓度系统
    </h1>
    <div class="loginContainer">
      <div class="loginForm">
        <van-field v-model="tel" placeholder="请输入手机号" :error-message="usertel" clearable />
        <van-field
          v-model="password"
          type="password"
          placeholder="请输入密码"
          :error-message="pass"
          clearable
        />
        <van-button
          type="primary"
          :loading="loading"
          loading-text="登录..."
          size="large"
          :disabled="zhud"
          @click="login"
        >登录</van-button>
      </div>
    </div>

    <div class="copyRight">
      <img src="../../assets/img/zkawlogo.svg" alt />
      <p>沈阳中科奥维科技股份有限公司</p>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { Field, Button, Toast, Divider } from 'vant'
Vue.use(Field)
Vue.use(Button)
Vue.use(Toast)
Vue.use(Divider)

export default {
  data() {
    return {
      tel: '',
      password: '',
      zhud: false,
      loading: false,
    }
  },
  created: function () {
    this.$emit('header', false)
  },
  computed: {
    usertel() {
      if (this.tel === '') {
        return ''
      } else if (!/^[1][3,4,5,7,8][0-9]{9}$/.test(this.tel)) {
        return '手机号格式错误'
      } else {
        return ''
      }
    },
    pass() {
      if (this.password === '') {
        return ''
      } else if (this.password.length < 6) {
        return '密码不可小于6位'
      } else {
        return ''
      }
    },
  },
  methods: {
    toRegister() {
      this.$router.push('/register')
    },
    login() {
      if (this.tel === '' || this.usertel === '手机号码格式错误') {
        Toast('手机号码输入有误')
        return
      }
      if (this.password === '' || this.pass === '密码格式错误，最少为6位') {
        Toast('密码输入有误')
        return
      }
      this.reallR()
    },
    reallR() {
      this.zhud = true
      this.loading = true
      this.$http({
        url: this.$http.adornUrl(`/app/login`),
        method: 'post',
        data: this.$http.adornData({
          account: this.tel,
          password: this.password,
        }),
      }).then(({ data }) => {
        this.zhud = false
        this.loading = false
        if (data && data.code === 0) {
          Toast('登录成功')
          localStorage.setItem('token', data.token)
          this.$router.replace('/overview')
          // Vue.cookie.set('token',data.token)
        } else {
          Toast(data.msg)
          // this.$router.back(); //登陆成功返回上一页
        }
      })
    },
  },
}
</script>

<style scoped>
.login-bg {
  width: 100%;
  height: 30vh;
  margin-bottom: 20px;
  background: url('../../assets/img/login.png') no-repeat bottom center;
  background-size: cover;
}

.system-title {
  text-align: center;
  line-height: 40px;
  font-size: 30px;
  font-weight: 600;
  color: #004e92;
}

.loginContainer {
  margin-top: 20px;
}
.loginForm {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.van-field {
  height: 30px;
  width: 200px;
  border-radius: 4px;
  border-style: none;
  background-color: #f5f5f5;
  margin: 10px;
  padding: 0;
  line-height: 30px;
}

div /deep/ .van-field__control {
  padding: 0 16px;
}

.van-button {
  width: 200px;
  height: 30px;
  margin-top: 20px;
  color: #fff;
  background-color: #1773c3;
  border-radius: 4px;
  border-color: #1773c3;
  text-align: center;
  line-height: 30px;
}

.copyRight {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 20px;
  text-align: center;
  z-index: -999;
}
.copyRight > p {
  margin-top: 4px;
  font-size: 8px;
  color: #969696;
}
.copyRight > img {
  width: 70px;
  stroke: #f5adad;
  margin-bottom: 4px;
}
</style>
