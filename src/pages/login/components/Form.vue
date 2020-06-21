<template>
  <form method="post" action="" ref="form">
    <img class="avatar"
    src="@/assets/img/default.png"
    >
    <!-- 有提示信息时展示 -->
    <div
    id="alert"
    :class = "[alert,alertStatus]"
    >
      {{message}}
    </div>
    <div class="form-group">
      <span class="login-icon">&#xe788;</span>
      <input
      id="username"
      name="username"
      class="icon login-input"
      placeholder="邮箱/手机"
      autofocus
      v-model="userVal"
      @focus="handleFocus"
      >
    </div>
    <div class="form-group">
      <span class="login-icon">&#xe61b;</span>
      <input
      id="password"
      name="password"
      type="password"
      class="icon login-input"
      placeholder="请输入密码"
      v-model="pwVal"
      @focus="handleFocus"
      >
    </div>
    <router-link to="/">
      <button
      class="btn"
      id="btn"
      @click="handleBtnClick"
      >
        登 录
      </button>
    </router-link>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  name: 'LoginForm',
  data () {
    return {
      userVal: '',
      pwVal: '',
      message: '',
      alert: '',
      alertStatus: ''
    }
  },
  methods: {
    postInfo () {
      axios.post('/api/user/login', {username: this.userVal, password: this.pwVal})
        .then(this.InfoSucc)
    },
    getInfo () {
      axios.get('/api/user/login', {
        params: {
          username: this.userVal,
          password: this.pwVal
        }
      }).then(this.InfoSucc)
    },
    InfoSucc (res) {
      res = res.data
      this.message = res.message
      this.alert = 'alert'
      if (this.message === '登录中...') {
        this.alertStatus = 'alert-success'
      } else {
        this.alertStatus = 'alert-danger'
      }
    },
    // 点击登录出现提醒
    handleBtnClick () {
      if (this.$refs.form.method === 'post') {
        this.postInfo()
      } else if (this.$refs.form.method === 'get') {
        this.getInfo()
      }
    },
    // 输入框获得焦点隐藏提醒
    handleFocus () {
      this.alert = ''
      this.alertStatus = ''
      this.message = ''
    }
  }
}
</script>

<style lang="stylus" scoped>
  .avatar
    position: absolute
    top: -60px
    left: 50%
    width: 120px
    height: 120px
    margin-left: -70px
    border: 10px solid #fff
    border-radius: 50%
    box-shadow: 0 1px 5px #ccc
  .alert
    padding: 15px
    margin: 0 20px 20px
    border: 1px solid #ebccd1
    border-radius: 4px
  .alert-danger
    background-color: #f2dede
    color: #a94442
  .alert-success
    background-color: #dff0d8
    border-color: #d6e9c6
    color: #3c763d
  .form-group
    margin-bottom: 15px
    .login-icon
      display: inline-block
      font-family: icon
      color: #666
      font-size: 1.5rem
      margin-right: 5px
    .login-input
      width: 77%
      height: 20px
      padding: 10px
      border: 1px solid  #cccbcb
      border-radius: 7px
      letter-spacing: 1px
      font-size: 10px
  .btn
    display: block
    /*overflow: hidden;*/
    width: 80%
    height: 30px
    margin: 0 auto
    line-height: 30px
    text-align: center
    cursor: pointer
    color: #ffffff
    background-color: #40586d
    border-color: #374b5d
    border: 1px solid transparent
  .btn:hover
    color: #ffffff
    background-color: #2d3e4d
    border-color: #202c36
</style>
