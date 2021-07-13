<template>
    <div>
      <el-button  @click="saveData()">
        <span>保存</span>
      </el-button>
      <el-form ref="add" :model="form" :validate-on-rule-change="false" :rules="rules" label-position="right">
        <el-row>
          <el-col :span="24">
            <el-form-item label="概要描述：" prop="noticeDescription" :label-width="formLabelWidth">
              <div class="ueditor-css" >
                <vue-ueditor-wrap v-model="form.noticeDescription" :config="myConfig"></vue-ueditor-wrap>
              </div>
            </el-form-item>
          </el-col>
        </el-row >
      </el-form>
    </div>
</template>

<script>
  import VueUeditorWrap from 'vue-ueditor-wrap'
    export default {
        components: {VueUeditorWrap},
        data(){
          return {
            formLabelWidth: '150px',
            myConfig: {
              // 如果需要上传功能,找后端小伙伴要服务器接口地址
              //serverUrl: this.$config.baseUrl + 'ueditor/ueditorConfig',
              // serverUrl: 'http://localhost:8090/ueditor/ueditorConfig',
              // 你的UEditor资源存放的路径,相对于打包后的index.html
              serverUrl: process.env.VUE_APP_HUSSAR_DEFAULT_API + '/public/ueditor/ueditorConfig',
              UEDITOR_HOME_URL: '/static/ueditor/',
              // 编辑器不自动被内容撑高
              autoHeightEnabled: false,
              // 工具栏是否可以浮动
              autoFloatEnabled: false,
              // 初始容器高度
              initialFrameHeight: 340,
              // 初始容器宽度
              initialFrameWidth: '100%',
              // 关闭自动保存
              enableAutoSave: true,
            },
            form:{
              noticeDescription:''
            },
            rules: {
              noticeDescription: [
                {required: true, message: '请输入', trigger: 'change'},
              ]
            },

          }
        },
      methods: {
        saveData() {
          this.$refs.add.validate((valid) => {
            if (valid) {
              console.log(this.form.noticeDescription);
            }
          })
        }
      }
    }
</script>

<style scoped>

</style>
