<template>
  <div class="login_container">
     <div class="login_box">
       <!-- 头像区域 -->
       <div class="avatar_box">
         <img src="../assets/logo.png" alt="">
       </div>
       <!-- 登陆表单区域 -->
       <el-form ref="loginFormRef" :model="loginForm" :rules="loginRules" label-width="80px" class="login_form">
         <!-- 用户名 -->
         <el-form-item prop="username" label="用户">
           <el-input v-model="loginForm.username"></el-input>
         </el-form-item>
         <!-- 密码 -->
         <el-form-item prop="password" label="密码">
           <el-input v-model="loginForm.password" type="password"></el-input>
         </el-form-item>
         <!-- 按钮 -->
         <el-form-item class="btns">
           <el-button type="primary" @click="login('loginFormRef')">登录</el-button>
           <el-button type="info" @click="resetLoginForm('loginFormRef')">重置</el-button>
         </el-form-item>
       </el-form>
     </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      // 这是表单的数据绑定对象
      loginForm: {
        username: '',
        password: ''
      },
      // 这是表单的验证规则对象
      loginRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm (formName) {
      this.$refs[formName].resetFields()
    },
    login (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$http.post('login', this.loginForm)
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_container{
  background-color: #2b4b6b;
  height: 100%;
}
.login_box{
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
}
.avatar_box{
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%,-50%);
  background-color: #fff;
  img{
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}
.login_form{
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
.btns{
  display: flex;
  justify-content: flex-end;
}
</style>
