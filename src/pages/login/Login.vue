<template>
  <div class="login">
    <div class="login-wrap">
      <login-form></login-form>
      <login-nav></login-nav>
    </div>
  </div>
</template>

<script>
import LoginForm from './components/Form'
import LoginNav from './components/Nav'
export default {
  name: 'Login',
  components: {
    LoginForm,
    LoginNav
  }
}
</script>

<style lang="stylus" scoped>
  .login
    background-color: #2f4050
    position: fixed
    width: 100%
    height: 100%
    .login-wrap
      position: relative
      max-width: 380px
      margin: 0 auto
      padding: 100px 40px 40px
      border-radius: 4px
      background-color: #fff
      top: 50%;
      transform: translateY(-50%)
</style>
