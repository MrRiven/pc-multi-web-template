<template>
  <el-card class="login-card">
    <div slot="header">
      <img :src="logo" class="logo-img">
      <span class="logo-text">Management System</span>
    </div>
    <el-form class="login" :rules="rules" ref="ruleForm" :model="ruleForm" label-width="100px" >
      <el-form-item label="Phone" prop="phone">
        <el-input placeholder="Please enter phone number" icon="my-phone" v-model="ruleForm.phone" type="tel" :maxlength="11"></el-input>
      </el-form-item>
      <el-form-item label="Password" prop="password">
        <el-input placeholder="Please enter password" icon="my-password" v-model="ruleForm.password" type="password" @keyup.enter="login"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="login">Login</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
  import logo from 'assets/img/logo.png'
  import { getInfo } from "@/common/api";
  export default {
    data () {
      return {
        logo: logo,
        ruleForm: {
          phone: '',
          password: ''
        },
        rules: {
          phone: [
             { required: true, message: 'Phone required', trigger: 'blur' }
          ],
          password: [
             { required: true, message: 'Password required', trigger: 'blur' }
          ]
        }
      }
    },
     created(){
        getInfo(
          {
      cartkey: "39b813508b44e73a66bfddbb0563f91e",
      demandcartkey: "39b813508b44e73a66bfddbb0563f91e",
      provinceid: 1,
      province: 1,
      provincename: "上海",
      tradername: "yw_app",
      trader: "h5",
      closesignature: "yes",
      signature_method: "md5",
      timestamp: "1521771333651",
      signature: "****",
      siteid: 0
    }
        )
      .then(response => {
         
        console.log(response);
      
      })
      .catch(error=>{
        console.log(error);
      });
     },
    methods: {
      login () {
        this.$refs.ruleForm.validate((valid) => {
          if (!valid) {
            return
          }
          location.assign('../user/index.html')
        })
      }
    }
  }
</script>

<style lang="scss">
  .login-card {
    width: 800px;
    margin: 100px auto;
    .login {
      display: block;
      width: 400px;
      margin: 100px auto;
    }
    .logo-img {
      width: 90px;
    }
    .logo-text {
      margin-left: 20px;
    }
  }

</style>
