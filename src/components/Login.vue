<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/logo.png" alt />
      </div>

      <el-form ref="LoginFormRef" :model="LoginForm"  :rules="LoginFormRules" label-width="0px" class="login_form">
        <el-form-item prop="username">
          <el-input v-model="LoginForm.username" prefix-icon="el-icon-user"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input v-model="LoginForm.password" prefix-icon="el-icon-lock" type="password"></el-input>
        </el-form-item>
        <el-form-item class="btns">
           <el-button type="primary" @click="login">登陆</el-button>
           <el-button type="info" @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      LoginForm: {
        username: 'soleperson',
        password: ''
      },
      LoginFormRules: {
        username: [
          { required: true, message: 'Input username', trigger: 'blur' },
          { min: 6, message: '长度不少于6', trigger: 'blur' }
        ],
        password: [
          { required: true, message: 'Input password', trigger: 'blur' },
          { min: 6, message: '长度不少于6', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm () {
      this.$refs.LoginFormRef.resetFields()
    },
    login () {
      this.$refs.LoginFormRef.validate(async (valid) => {
        // eslint-disable-next-line no-useless-return
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.LoginFormRef)
        console.log(res)
      })
    }
  }
}
</script>

<style lang='less' scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  width: 450px;
  height: 300px;
  background-color: #ffffff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eeeeee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #dddddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #ffffff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eeeeee;
    }
  }
}
.btns{
    display: flex;
    justify-content: flex-end;
}
.login_form{
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
}
</style>
