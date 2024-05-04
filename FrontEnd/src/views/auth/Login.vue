<template>
  <div class="background">
    <a-form
      id="components-form-normal-login"
      :form="form"
      class="login-form"
      @submit="handleSubmit"
    >
      <div class="image-container">
        <img src="../../assets/logo.jpg" alt="Image" class="image" />
      </div>
      <a-form-item>
        <a-input
          v-decorator="[
            'phone',
            {
              rules: [{ required: true, message: '请输入您的手机号!' }],
            },
          ]"
          placeholder="手机号账号"
        >
          <a-icon
            slot="prefix"
            type="user"
            style="color: rgba(0, 0, 0, 0.25)"
          />
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-input
          v-decorator="[
            'password',
            {
              rules: [{ required: true, message: '请输入您的密码！' }],
            },
          ]"
          type="password"
          placeholder="密码"
        >
          <a-icon
            slot="prefix"
            type="lock"
            style="color: rgba(0, 0, 0, 0.25)"
          />
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-checkbox
          v-decorator="[
            'remember',
            {
              valuePropName: 'checked',
              initialValue: false,
            },
          ]"
        >
          记住我
        </a-checkbox>
        <a class="login-form-forgot" href=""> 忘记密码 </a>
        Or
        <a @click="to_register"> 注册 </a>
      </a-form-item>
      <a-form-item>
        <a-button
          type="primary"
          size="large"
          html-type="submit"
          class="login-form-button"
        >
          登录
        </a-button>
      </a-form-item>
    </a-form>
  </div>

</template>

<script>
export default {
  name: "Login",
  data() {
    return {};
  },
  beforeCreate() {
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    handleSubmit(e) {
      // 提交数据
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          let data = {
            phone: values["phone"],
            password: values["password"],
          }
          this.$user_info.login(data).then((res) => {
            // 请求后端数据
            if (res.code == 200) {
              localStorage.token = res.data.token
              this.$message.success('登录成功！')
              this.$router.go(0)
            } else {
              this.$message.error(res.msg)
            }
          });
        }
      });
    },
    to_register() {
      // 页面跳转
      this.$router.push({
        path: `/register`,
      });
    },
  },
};
</script>

<style scoped>
.background {
  /* 设置背景图样式 */
  background-image: url('../../assets/beijing.jpg');
  background-size: cover;
  background-position: center;
  /* 充满整个屏幕 */
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* 使登录框内容垂直水平居中 */
  display: flex;
  justify-content: center;
  align-items: center;
}
.image-container {
  text-align: center;
  margin-bottom: 20px; /* 调整图片与输入框之间的距离 */
}

.image {
  width: 250px; /* 根据需要调整图片大小 */
  height: auto;
}
#components-form-normal-login {
  min-width: 450px;
  width: 600px;
  margin: 8rem auto;
}

#components-form-normal-login .login-form-forgot {
  float: right;
}

#components-form-normal-login .login-form-button {
  width: 100%;
}
</style>
