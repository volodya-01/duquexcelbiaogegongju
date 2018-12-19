<template>
	<div>
	
			<div class="box">
				<!--上传文件模块-->
					<el-upload class="upload-demo" :show-file-list=false action="" drag :before-upload="acceptFile">
					<i class="el-icon-upload"></i>
					<div class="el-upload__text">将文件拖到此处，或<em>点击上传。</em></div>
					</el-upload>
			</div>
		<div>
					{{this.arr}}
				</div>
	</div>
</template>
<script>
import XLSX from "xlsx";
export default {
  name: "app",
  data() {
    return {
      arr: []
    };
  },
  methods: {
    acceptFile(f) {
      //获取到文件名最后一个"."的位置
      let extStart = f.name.lastIndexOf(".");
      //通过未知 获取文件后缀名
      let filetype = f.name.substring(extStart, f.name.length).toUpperCase();
      //如果后缀名不是 excel文件 提示上传指定文件
      if (filetype != ".XLSX" && filetype != ".XLS") {
        alert("请上传正确的文件格式");
        return;
      }
      //格式正确后 开始对文件进行操作
      this.handleFile(f);
    },
    handleFile(f) {
      if (window.FileReader) {
        //如果浏览器支持 创建fileReader
        var reader = new FileReader();
      } else {
        this.$message.error("你的浏览器不支持fileReader,请升级您的浏览器！");
      }
      reader.onload = e => {
        let data = e.target.result,
          //使用XLSL控件 读取文件信息
          workbook = XLSX.read(data, { type: "binary" }),
          //获取到excel里第一个sheet文件
          sheetName = workbook.SheetNames[0],
          //获取到sheet内容
          sheet = workbook.Sheets[sheetName];
        self.data = XLSX.utils.sheet_to_json(sheet);
        var tabl = self.data;
        var value = [];

        var i;
        for (i = 0; i <= self.data.length - 1; i++) {
          value.push(parseFloat(self.data[i].值));
        }
        console.log(value);
        this.arr = value;
      };

      //将文件读取为二进制码
      reader.readAsBinaryString(f);
    }
  }
};
</script>

<style scoped>
.box {
	margin-top: -50px;
  padding: 100px 800px 0 800px;
}
</style>