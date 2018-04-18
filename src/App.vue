<template>
  <div id="app">
    <my-header></my-header>
    <div class="tab">
      <div class="tab-item"><router-link to="/goods">商品</router-link></div>
      <div class="tab-item"><router-link to="/ratings">评论</router-link></div>
      <div class="tab-item"><router-link to="/seller">商家</router-link></div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import Header from "./components/header/header.vue"

  export default {
    components:{
        "my-header": Header,
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" >
  #app
    .tab
      display: flex
      flex-direction: row
      width:100%
      height:40px;
      line-height:40px;
      .tab-item
        flex:1
        text-align: center
        font-size :14px
        &>a
          display : block
          text-decoration : none
          &.router-link-active
            color: #f01414


</style>
