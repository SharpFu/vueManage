<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 文件上传</el-breadcrumb-item>
                <el-breadcrumb-item>学习资料上传</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="plugins-tips">
            学习资料放在这里，方便大家下载O(∩_∩)O~
        </div>
        <el-upload
          class="upload-file-container"
          action="http://localhost:3000/upload/uploading"
          accept="image/*"
          :on-preview="handlePreview"
          :on-remove="handleRemove"
          :on-success="handleSuccess"
          :on-error="handleError"
          :file-list="fileList">
          <el-button size="small" type="primary">点击上传</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data: function(){
            return {
                fileList: []
            }
        },
        beforeMount() {
            this.loadAllFile();
        },
        methods:{
            handleRemove(file, fileList) {
                this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
                  confirmButtonText: '确定',
                  cancelButtonText: '取消',
                  type: 'warning'
                }).then(() => {
                    console.log(JSON.stringify(file));
                   axios.get("http://localhost:3000/upload/delete",{params:{name:file.name}}).then(res =>{
                       if(res.data.code==200){
                           this.$message({
                                type: 'success',
                                message: '删除成功!'
                            });
                           this.loadAllFile();
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
            
              },
            handlePreview(file) {
                console.log(file);
            },
            handleSuccess(response, file, fileList){
                console.log(file);
            },
            handleError(err, file, fileList){
                console.log(JSON.stringify(err)+"====="+file);
            },
            /*获取所有文件*/
            loadAllFile(){
                var _this = this;
                _this.fileList=[];
                axios.get("http://localhost:3000/upload/getAll").then(res =>{
                    res.data.forEach(function(item){
                        _this.fileList.push({
                            name:item.fileName,
                            url:item.path
                        })
                    });
                });
            }
            
        }
    }
</script>

<style scoped>
    
</style>