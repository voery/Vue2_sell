<template>
  <div id="app">
    <!-- 传值 -->
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <!-- 链接 -->
        <router-link :to="{path:'/goods'}">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{path:'/ratings'}">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{path:'/seller'}">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
  // 应用组件
  import header from './components/header/header.vue';
  const ERR_OK = 0;
export default {
  data() {
    return {
      seller: {} // 初始化数据
    };
  },
  // 生命周期在创建的时候调用
  created() {
    // get请求获取seller数据
    this.$http.get('/api/seller').then((response) => {
     response = response.body; // 请求的数据在response.body中
     if (response.erron === ERR_OK) {
       this.seller = response.data;
     }
    });
  },
  components: {
    'v-header': header // 申明要调用的组件
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  // 引用外部的styl文件
  @import "./common/stylus/mixin.styl"

#app
  .tab
    display : flex
    width:100%
    height: 40 px
    line-height:40px
    // border-bottom : 1px solid rgba(7,17,27,0.1)
    border-1px(rgba(7,17,27,0.1))
    .tab-item
      flex :1
      text-align :center
      & > a
        display : block
        font-size : 14px
        color: rgb(77,85,93)
        &.active
          color: rgb(240,20,20)
</style>
