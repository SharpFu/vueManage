<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-setting"></i> 自述</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="ms-doc">
            <h3>关于我们</h3>
            <article>
                <h2>写在前面的话</h2>
                <p>九鼎瑞信前端团队目前有10人，未完待续.......</p>
                <h2>参与过的项目</h2>
                <div class="project">
                    <el-row>
                      <el-col :span="6" class="item" v-for="(o, index) in 6" :offset="(index % 3) > 0 ? 1 : 0">
                        <el-card :body-style="{ padding: '0px' }">
                          <img src="../../../static/img/keshihua.jpg" class="image">
                          <div style="padding: 14px;">
                            <span>大数据可视化平台</span>
                            <div class="bottom clearfix">
                                <!--<time class="time">{{ currentDate }}</time>-->
                              <el-button type="text" class="button">去看看</el-button>
                            </div>
                          </div>
                        </el-card>
                      </el-col>
                    </el-row>
                </div>
                <br>
                <br>
                <h2>联系我们</h2>
                <span>我们的QQ群:526896360</span>
                <br>
            </article>
        </div>

    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                
            }
        }
    }
</script>

<style scoped>
    .ms-doc{
        width:100%;
        max-width: 980px;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
    }
    .ms-doc h3{
        padding: 9px 10px 10px;
        margin: 0;
        font-size: 14px;
        line-height: 17px;
        background-color: #f5f5f5;
        border: 1px solid #d8d8d8;
        border-bottom: 0;
        border-radius: 3px 3px 0 0;
    }
    .ms-doc article{
        padding: 45px;
        word-wrap: break-word;
        background-color: #fff;
        border: 1px solid #ddd;
        border-bottom-right-radius: 3px;
        border-bottom-left-radius: 3px;
    }
    .ms-doc article h1{
        font-size:32px;
        padding-bottom: 10px;
        margin-bottom: 15px;
        border-bottom: 1px solid #ddd;
    }
    .ms-doc article h2 {
        margin: 24px 0 16px;
        font-weight: 600;
        line-height: 1.25;
        padding-bottom: 7px;
        font-size: 24px;
        border-bottom: 1px solid #eee;
    }
    .ms-doc article p{
        margin-bottom: 15px;
        line-height: 1.5;
    }
    .ms-doc article .el-checkbox{
        margin-bottom: 5px;
    }
    .ms-doc .image {
        width: 100%;
        display: block;
      }
      .project .item{
          margin-bottom: 10px;
      }
</style>