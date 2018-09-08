<template>
  <div>
    <div class="login-wrap" v-show="showLogin">
      <!-- 布局视图 -->
      <ul>
        <li v-if="!success">
          <p v-show="showPrompt">{{prompt}}</p>
          <input type="text" placeholder="请输入用户名" v-model="account">
          <input type="password" placeholder="请输入密码" v-model="password">
          <button v-on:click="login">登录</button>
        </li>
        <li v-if="success">
          <h3> 恭喜您，账号:</h3>
          <a>【{{account}}】</a>
          <h3> 登陆成功!</h3>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
  .login-wrap {
    text-align: center;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 10px 0;
  }

  a {
    color: #42b983;
    font-size: 26px;
  }

  p {
    color: red;
  }

  input {
    display: block;
    width: 250px;
    height: 40px;
    line-height: 40px;
    margin: 0 auto 10px;
    outline: none;
    border: 1px solid #888;
    padding: 10px;
    box-sizing: border-box;
  }

  button {
    display: block;
    width: 250px;
    height: 40px;
    line-height: 40px;
    border: none;
    background-color: #41b883;
    color: #fff;

    font-size: 16px;
    margin: 30px auto 5px;
  }

  span {
    cursor: pointer;
  }

  span:hover {
    color: #41b883;
  }

</style>

<script>
export default {
  data () {
    return {
      success: false,
      showLogin: true,
      showPrompt: false,
      prompt: '',
      account: '',
      password: ''
    }
  },
  methods: {
    // 登陆接口
    login: function () {
      if (this.account === '' || this.password === '') {
        alert('请输入用户名或密码')
      } else {
        // 参数传递
        let data = {'account': this.account, 'password': this.password, 'sign': 'abcd'}
        this.$http.post('/api/app/login/check', data)
          .then(res => {
            // 打印输出请求数据
            console.log(res.data.data)
            // 登陆成功
            this.success = true
          })
          .catch(error => {
            // 打印输出错误信息
            console.log(error)
            this.success = false
          })
      }
    }
  }
}
</script>
