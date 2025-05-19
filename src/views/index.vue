<template>
  <div class="app-container home">
    <el-row :gutter="20">
      <el-col :sm="24" :lg="24" style="padding: 20px">
        <h2>若依后台管理框架</h2>
        <p>
          <b>当前版本:</b> <span>v{{ version }}</span>
        </p>
      </el-col>
    </el-row>
    <el-divider />
    <el-row :gutter="20">
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-card class="main-content">
          <template v-slot:header>
            <div class="clearfix">
              <span>主要内容</span>
            </div>
          </template>
          <div class="body">
            <p>欢迎使用若依管理系统</p>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script setup name="Index">
import { getCurrentInstance } from 'vue'

const { proxy } = getCurrentInstance()
const version = ref('')

function goTarget(url) {
  window.open(url, "_blank");
}

function getVersion() {
  proxy.$http.get("https://gitee.com/api/v5/repos/y_project/RuoYi-Vue/tags").then(res => {
    version.value = res.data[0].name;
  });
}

onMounted(() => {
  getVersion();
});
</script>

<style scoped lang="scss">
.home {
  blockquote {
    padding: 10px 20px;
    margin: 0 0 20px;
    font-size: 17.5px;
    border-left: 5px solid #eee;
  }
  hr {
    margin-top: 20px;
    margin-bottom: 20px;
    border: 0;
    border-top: 1px solid #eee;
  }
  .col-item {
    margin-bottom: 20px;
  }

  ul {
    padding-left: 50px;
    li {
      line-height: 2;
    }
  }

  .update-log {
    ol {
      display: block;
      list-style-type: decimal;
      margin-block-start: 1em;
      margin-block-end: 1em;
      margin-inline-start: 0px;
      margin-inline-end: 0px;
      padding-inline-start: 40px;
    }
  }
}
</style>

