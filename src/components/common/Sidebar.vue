<template>
    <div class="sidebar">
        <!--<div class="user-info">
            <img class="user-logo" src="../../../static/img/jd_logo.png">
            <p>九鼎瑞信前端团队</p>
        </div>-->
        <div class="user-info">
            <div class="round">
                <div class="test"></div>
            </div>
            <div class="logo-img" title="九鼎瑞信"></div>
             <p>九鼎瑞信前端团队</p>
        </div>
        <el-menu :default-active="onRoutes" class="el-menu-vertical-demo" theme="dark" unique-opened router>
            <el-menu-item index="readme">
                <i class="el-icon-setting"></i>自述
            </el-menu-item>
            <el-submenu index="2">
                <template slot="title"><i class="el-icon-menu"></i>技术</template>
                <el-menu-item index="html5">html5</el-menu-item>
                <el-menu-item index="css3">css3</el-menu-item>
                <el-menu-item index="javascript">javascript</el-menu-item>
                <el-menu-item index="angularjs">angularjs</el-menu-item>
                <el-menu-item index="vue">vue</el-menu-item>
                <el-menu-item index="react">react</el-menu-item>
            </el-submenu>
            <el-submenu index="3">
                <template slot="title"><i class="el-icon-date"></i>技术分享</template>
                <el-menu-item index="notelist">所有笔记</el-menu-item>
                <el-menu-item index="note">写笔记</el-menu-item>
                <el-menu-item index="upload">文件上传</el-menu-item>
            </el-submenu>
            <el-submenu index="4">
                <template slot="title"><i class="el-icon-star-on"></i>三方库</template>
                <el-menu-item index="echarts">echarts</el-menu-item>
            </el-submenu>
            <el-submenu index="5">
                <template slot="title"><i class="el-icon-star-on"></i>小工具</template>
                <el-menu-item index="toolsdownload">工具下载</el-menu-item>
            </el-submenu>
            <el-submenu index="6">
                <template slot="title"><i class="el-icon-star-on"></i>优秀站点</template>
                <el-menu-item index="website">优秀站点</el-menu-item>
                <el-menu-item index="elementUI">elementUI</el-menu-item>
            </el-submenu>
        </el-menu>
    </div>
</template>

<script>
    export default {
        computed:{
            onRoutes(){
                return this.$route.path.replace('/','');
            }
        }
    }
</script>

<style scoped>
    .sidebar{
        display: block;
        position: absolute;
        width: 250px;
        left: 0;
        top: 70px;
        bottom:0;
        background: #2E363F;
    }
    .sidebar > ul {
        height:100%;
    } 
    .user-info {
        padding-top: 10px;
        width: 100%;
        height: 140px;
        text-align: center;
        background: #324157;
        color: #bfcbd9;
        font-size: 14px;
        border-bottom: 1px solid #bfcbd9;
    }
    .logo-img{
        width:80px ;
        height: 80px;
        background: url('../../../static/img/jd_logo.png') no-repeat;
        background-position: center;
        position: absolute;
        top: 20px;
        left: 85px;
    }
    .user-info .user-logo{
        margin-top: 20px;
        width:80px;
        height:80px;
        border-radius: 50%;
    }
    .user-info .round  {
    height: 100px;
    width: 100px;
    border: 1px solid #20a0ff;
    border-radius: 50%;
    display: inline-block;
    animation: rond 3s infinite;
    -webkit-animation: rond 3s infinite;
   }
   .user-info .test {
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
