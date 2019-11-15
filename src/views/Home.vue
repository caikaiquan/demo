<template>
  <div class="home">
    <div class="nav-list">
      <div class="item">
        <router-link to='/sweepcode'>扫码枪扫码</router-link>
      </div>
      <div class="item">
        <router-link to='/colorpicker'>图片转base64</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  }
}
</script>
<style lang="scss">
.nav-list{
  width: 980px;
  margin: 0 auto;
  padding-top: 30px;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  .item{
    padding: 0 20px;
    margin-bottom: 20px;
    cursor: pointer;
  }
}
</style>
