<template>
  <div class="sweep-cod">
    <h1>这里是扫码枪事件Demo</h1>
    <el-table :data="tableData" height="250" border style="width: 600px">
      <el-table-column type="index" width="50" label='编号'></el-table-column>
      <el-table-column prop="time" label="时间" width="180"></el-table-column>
      <el-table-column prop="value" label="条码" width="180"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      keycode: "",
      lastTime: null,
      nextTime: null,
      lastCode: null,
      nextCode: null,
      tableData: []
    };
  },
  created() {
    document.addEventListener("keydown", this.handleKeyDown);
  },
  mounted(){
    console.log(this.handleCountTime());
  },
  methods: {
    // 扫码事件
    handleKeyDown(e) {
      // 当前输入的code
      let nowcode;
      // 兼容处理
      if (window.event) {
        nowcode = e.keyCode;
      } else if (e.which) {
        nowcode = e.which;
      }
      // 获取当前时间
      let nowTime = new Date().getTime();
      // 条码存在 输入时间小于30毫秒 以回车结束  判断认定为扫码结束
      if (
        nowcode === 13 &&
        this.keycode != "" &&
        nowTime - this.lastTime <= 30
      ) {
        console.log(this.keycode);
        this.tableData.push({time:this.handleCountTime(),value:this.keycode})
        this.keycode = "";
        this.lastCode = null;
        this.lastTime = null;
      } else {
        if (this.lastTime == null && this.lastCode == null) {
          // 初始化赋值
          this.keycode = String.fromCharCode(nowcode);
        } else if (
          this.lastCode != null &&
          this.lastTime != null &&
          nowTime - this.lastTime <= 30
        ) {
          this.keycode += String.fromCharCode(nowcode);
        } else {
          this.keycode = "";
          this.lastCode = null;
          this.lastTime = null;
        }
        this.lastCode = nowcode;
        this.lastTime = nowTime;
      }
    },
    // 计算时间
    handleCountTime(){
      let date = new Date();
      let year = date.getFullYear();
      let month = date.getMonth() + 1;
      let day = date.getDate();
      let hh = date.getHours();
      let mm = date.getMinutes();
      let ss = date.getSeconds();
      return `${year}-${month}-${day} ${hh}:${mm}:${ss}`
    }
  },
  beforeDestroy() {
    document.removeEventListener("keydown", this.handleKeyDown);
  }
};
</script>

<style lang='scss' scoped>
</style>
