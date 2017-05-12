<template>
    <div class="login-wrap">
        <div class="ms-logo">
            <div class="round">
                <div class="test"></div>
            </div>
            <div class="logo-img" title="九鼎瑞信"></div>
        </div>
        
        <div class="ms-title">九鼎瑞信前端团队</div>
        <div class="ms-login">
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="0px" class="demo-ruleForm">
                <el-form-item prop="username">
                    <el-input v-model="ruleForm.username" placeholder="username"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input type="password" placeholder="password" v-model="ruleForm.password" @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>
                <div class="login-btn">
                    <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
                </div>
                <p style="font-size:12px;line-height:30px;color:#999;">Tips : 用户名密码随便填。</p>
            </el-form>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                ruleForm: {
                    username: '',
                    password: ''
                },
                rules: {
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
            submitForm(formName) {
                const self = this;
                self.$refs[formName].validate((valid) => {
                    if (valid) {
                        localStorage.setItem('ms_username',self.ruleForm.username);
                        self.$router.push('/readme');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .login-wrap{
        position: relative;
        width:100%;
        height:100%;
    }
    .ms-logo,.ms-title{
        position: absolute;
        top: 50%;
        text-align: center;
    }
    .ms-logo{
        left: 50%;
        margin-left: -50px;
        margin-top: -320px;
    }
    .logo-img{
        width:80px ;
        height: 80px;
        background: url('../../../static/img/jd_logo.png') no-repeat;
        background-position: center;
        border-radius: 50%;
        position: absolute;
        left: 10px;
        top: 10px;
    }
    .ms-title{
        width: 100%;
        margin-top: -200px;
        font-size: 16px;
        color: #fff;
    }
    .ms-login{
        position: absolute;
        left:50%;
        top:50%;
        width:300px;
        height:160px;
        margin:-150px 0 0 -190px;
        padding:40px;
        border-radius: 5px;
        background: #fff;
    }
    .login-btn{
        text-align: center;
    }
    .login-btn button{
        width:100%;
        height:36px;
    }
    .ms-logo .round  {
    height: 100px;
    width: 100px;
    border: 1px solid #20a0ff;
    border-radius: 50%;
    position: absolute;
    animation: rond 3s infinite;
    -webkit-animation: rond 3s infinite;
   }
   .ms-logo .test {
    height: 10px;
    width: 10px;
    position: absolute;
    background-color: #20a0ff;
    border-radius: 50%;
    top: 0px;
    left: 10px;
    margin: 5px;
}
@keyframes rond {
  0% {transform : rotate(0deg);}
  100% {transform : rotate(360deg);}
}

@-webkit-keyframes rond {
    0%{-webkit-transform : rotate(0deg);}
  100%{-webkit-transform : rotate(360deg);}
}
</style>