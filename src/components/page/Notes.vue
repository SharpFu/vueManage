<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 技术分享</el-breadcrumb-item>
                <el-breadcrumb-item>写笔记</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="plugins-tips">
            你的每一次分享，可能会让小伙伴跳过一个大坑 O(∩_∩)O
        </div>
        <div class="form-box">
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="标题">
                    <el-input v-model="form.title"></el-input>
                </el-form-item>
                <el-form-item label="内容">
                     <markdown-editor v-model="form.content" :configs="configs" ref="markdownEditor"></markdown-editor>
                </el-form-item>
                <el-form-item label="分类">
                    <el-radio-group v-model="form.type">
                        <el-radio label="0"  >html</el-radio>
                        <el-radio label="1"  >css</el-radio>
                        <el-radio label="2"  >javascript</el-radio>
                        <el-radio label="3"  >vue</el-radio>
                        <el-radio label="4"  >angularjs</el-radio>
                        <el-radio label="5"  >react</el-radio>
                        <el-radio label="6"  >微信小程序</el-radio>
                        <el-radio label="7"  >其他三方库</el-radio>
                        <el-radio label="8"  >小工具使用</el-radio>
                    </el-radio-group>
                </el-form-item>
                <el-form-item label="难度系数">
                    <el-rate v-model="form.easy" :colors="['#99A9BF', '#F7BA2A', '#FF9900']"></el-rate>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">提交</el-button>
                    <el-button>取消</el-button>
                </el-form-item>
               
            </el-form>
        </div>
    </div>
</template>

<script>
    import { markdownEditor } from 'vue-simplemde';
    import axios from 'axios';
    export default {
        data: function(){
            return {
                content:'',
                form:{
                    title:'',
                    content:'',
                    type:"html",
                    easy:0
                },
                configs: {
                    status: true,
                    initialValue: '',
                    renderingConfig: {
                        codeSyntaxHighlighting: true,
                        highlightingTheme: 'atom-one-light'
                    }
                }
            }
        },
        methods:{
            onSubmit:function(){   /*点击提交,保存数据*/
               var self = this;
                axios.get("http://localhost:3000/note/addNote",{params:this.form}).then(res =>{
                    if(res.data.code==200){
                        this.$message({
                          message: '添加成功',
                          type: 'success'
                        });
                        self.$router.push('/notelist');
                    }else{
                        this.$message.error('添加失败，赶紧去找找原因吧^_^');
                    }
                })
            }
        },
        components: {
            markdownEditor
        }
    }
</script>
<style type="text/css">
	.form-box{
	    width: 1000px;
	}
	.el-rate {
        height: 36px;
        line-height: 36px;
    }
</style>
