<template>
  <div class="rqcode">
    <h1>这里是生成二维码页面</h1>
    <div class="container">
      <p>
        <el-input v-model.trim="value"></el-input>
      </p>
      <p>
        <el-button type="primary" @click="handleqrcode">生成二维码</el-button>
      </p>
      <p>
        <el-button type @click="handleClear">清空</el-button>
      </p>
    </div>
    <div id="qrcode"></div>

    <sweep-code></sweep-code>
  </div>
</template>

<script>
import QRCode from "qrcodejs2";
import SweepCode from './SweepCode.vue'
export default {
    components:{SweepCode},
  data() {
    return {
      value: "",
      qrcode: ""
    };
  },
  mounted() {},
  methods: {
    handleqrcode() {
      if (!this.value) {
        return;
      }
      if (this.qrcode) {
        this.qrcode.clear();
        this.qrcode.makeCode(this.value);
        return;
      }

      let qrcode = new QRCode("qrcode", {
        width: 132,
        height: 132,
        text: this.value, // 二维码地址
        colorDark: "#000",
        colorLight: "#fff",
      });

      this.qrcode = qrcode;
    },
    handleClear() {
      if (this.qrcode) {
        document.querySelector("#qrcode").innerHTML = "";
      }
      this.value = "";
    }
  }
};
</script>

<style lang='scss' scoped>
.rqcode {
  width: 500px;
  margin: 0 auto;
}
.container {
  display: flex;
  p + p {
    margin-left: 20px;
  }
}
</style>