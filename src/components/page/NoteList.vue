<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 技术分享</el-breadcrumb-item>
                <el-breadcrumb-item>笔记列表</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="plugins-tips">
            你的每一次分享，可能会让小伙伴跳过一个大坑 O(∩_∩)O
        </div>
        <div class="noteList" v-loading.body="loading" >
            <section v-for="(item,index) in notes"  @mouseover="showBtn(index)" @mouseout="hideBtn(index)">
                <h3>{{item.title}}</h3>
                <div class="item-tag">
                	<span>类型：{{types[item.type]}} </span>
                	<span>难度系数：<el-rate disabled show-text v-model="item.easy" :colors="['#99A9BF', '#F7BA2A', '#FF9900']" ></el-rate></span>
                </div>
                <p  class="item-content" v-html="item.content"></p>
                <span class="btns" v-show="btnStatus==index">
                    <el-button :plain="true" type="danger" @click="deleteNote(item.id)">删除</el-button>
                    <el-button :plain="true" type="info">编辑</el-button>
                  </span>
            </section>
        </div>
        <el-pagination  @size-change="handleSizeChange"  @current-change="handleCurrentChange"  :current-page.sync="currentPage"  :page-size="100"  layout="total, prev, pager, next"  :total="1000"></el-pagination>
    </div>
</template>

<script>
    import axios from 'axios';
    import marked from 'marked';
     export default {
        data: function(){
            return {
               btnStatus:"",
               currentPage: 1,
               notes:[],
               loading:false,
               types:["html","css","javascript","vue","angularjs","react","微信小程序","其他三方库","小工具使用"]
            }
        },
        filters:{
             typeFilter:function(value,types){
                 console.log("test filter");
                 return types[value];
             }
        },
        beforeMount(){
            marked.setOptions({
              renderer: new marked.Renderer(),
              gfm: true,
              tables: true,
              breaks: false,
              pedantic: false,
              sanitize: false,
              smartLists: true,
              smartypants: false
            });
            this.loadData();
        },
        methods:{
            loadData () {
                var _this = this;
                this.loading=true;
                axios.get("http://localhost:3000/note/getAll").then(res =>{
                    _this.notes = res.data;
                    this.loading=false;
                })
            },
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
              },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
                this.loadData();
              },
            showBtn(index){
                this.btnStatus=index;
            },
            hideBtn(index){
                this.btnStatus="";
            },
            deleteNote(thisId){
                this.$confirm('此操作将永久删除该记录, 是否继续?', '提示', {
                  confirmButtonText: '确定',
                  cancelButtonText: '取消',
                  type: 'warning'
                }).then(() => {
                   axios.get("http://localhost:3000/note/delete",{params:{id:thisId}}).then(res =>{
                       if(res.data.code==200){
                           this.$message({
                                type: 'success',
                                message: '删除成功!'
                            });
                           this.loadData();
                       }else{
                           this.$message({
                                type: 'danger',
                                message: '删除失败!'
                            });
                       }
                   })
                }).catch(() => {
                  this.$message({
                    type: 'info',
                    message: '已取消删除'
                  });          
                });
            }
        }
    }
</script>

<style>
    .noteList section{
            padding: 20px 8px;
            border-top:1px solid #ddd;
            font-size: 14px;
            position: relative;
    }
    .item-tag{
        height: 25px;
        line-height: 25px;
    }
    .item-tag>span{
        margin-right:20px;
    }
    .el-rate{
        display: inline-block;
        height: 100%;
        line-height: 100%;
    }
    .item-content{
        padding:5px 0;
    }
    .item-tag,.item-content{
        color: #999999;
    }
    .el-pagination{
        text-align: center;
        width: calc(100% - 50px);
    }
    .btns{
        position: absolute;
        right: 0;
        top: 20px;
    }
</style>