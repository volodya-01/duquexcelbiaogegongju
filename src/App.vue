<template>
    <div id="app">
    	<div class="tex">nodejs 读取本地excel文件(指定格式)。若无模板点击此处<a href="static/test.xlsx" style="cursor:pointer;color:#409EFF;text-decoration: underline;">下载</a></div>
       	<file-reader></file-reader>
    </div>
</template>

<script>
import FileReader from "./components/fileReader.vue";
export default {
  name: "app",
  data() {
    return {};
  },
  components: {
    FileReader
  }
};
</script>
<!--App.vue是项目入口文件。-->
<style type="text/css">
.tex {
  width: 100vw;
  height: 60px;
  line-height: 60px;
  text-align: center;
  margin-top: 100px
}
i {
  color: "#409EFF";
}
</style>