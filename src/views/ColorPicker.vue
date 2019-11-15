<template>
  <div class="color-picker">
    <div class="title">图片转base64</div>
    <div class="upload-img">
      <p>请选择一张本地图片：</p>
      <div class="btn">
        <el-button type="primary">
          上传图片
          <input type="file" @change="handleChange" />
        </el-button>
      </div>
      
      <div class="img-box">
        <p>图片预览：</p>
        <div class="img-content">
          <img :src="imgUrl" alt id="img" />
        </div>
      </div>
      <div class="base64-box">
        <el-button @click='handleGenerate'>生成base6</el-button>
        <textarea class="base64-url" name id cols="30" rows="10" v-model="base64Url"></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imgUrl: "",
      base64Url: ""
    };
  },
  methods: {
      
    handleChange(e) {
      let files = e.target.files;
      let url = window.URL.createObjectURL(files[0]);
      this.imgUrl = url;
      this.base64Url = this.getImageBase64(document.querySelector("#img"), "png");
    },
    handleGenerate(){
        this.base64Url = this.getImageBase64(document.querySelector("#img"), "png");
    },
    getImageBase64(img, ext) {
      var canvas = document.createElement("canvas"); //创建canvas DOM元素，并设置其宽高和图片一样
      canvas.width = img.width;
      canvas.height = img.height;
      var ctx = canvas.getContext("2d");
      ctx.drawImage(img, 0, 0, img.width, img.height); //使用画布画图
      var dataURL = canvas.toDataURL("image/" + ext); //返回的是一串Base64编码的URL并指定格式
      canvas = null; //释放
      return dataURL;
    }
  }
};
</script>

<style lang='scss'>
.color-picker {
  .title {
    height: 50px;
    line-height: 50px;
    font-size: 22px;
    text-align: center;
  }

  .upload-img {
    .btn {
      position: relative;
      input {
        width: 98px;
        height: 40px;
        position: absolute;
        top: 0;
        left: 0;
        opacity: 0;
      }
    }

    .img-box {
      width: 50%;
      float: left;
    }

    .img-content {
      width: 100%;
      height: 400px;
      border: 1px solid #ccc;
      border-radius: 5px;
      overflow: auto;
      /*滚动条整体样式*/
      &::-webkit-scrollbar {
        width: 10px;
        height: 10px;
      }
      /*滚动条滑块*/
      &::-webkit-scrollbar-thumb {
        border-radius: 10px;
        -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
        background: #e1e1e1;
      }
      /*滚动条轨道*/
      &::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 1px rgba(221, 137, 137, 0);
        border-radius: 10px;
        background: #f5f5f5;
      }
    }
    .base64-box {
      width: 50%;
      float: right;
      button{
          margin-bottom: 13px;
      }
      .base64-url {
        width: 100%;
        height: 400px;
        border: 1px solid #ccc;
        overflow: auto;
        &::-webkit-scrollbar {
          width: 10px;
          height: 10px;
        }
        /*滚动条滑块*/
        &::-webkit-scrollbar-thumb {
          border-radius: 10px;
          -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
          background: #e1e1e1;
        }
        /*滚动条轨道*/
        &::-webkit-scrollbar-track {
          -webkit-box-shadow: inset 0 0 1px rgba(221, 137, 137, 0);
          border-radius: 10px;
          background: #f5f5f5;
        }
      }
    }
  }
}
</style>