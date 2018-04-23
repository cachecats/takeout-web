<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="name">{{item.name}}</span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper"></div>
  </div>
</template>

<script>
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data(){
      return {
        goods: {}
      }
    },
    created(){
      this.$http.get('static/data.json').then((res) => {
        this.goods = res.body.goods;
      })
    }

  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .goods
    display: flex
    flex-direction: row
    position: absolute
    width: 100%
    top: 174px
    bottom: 46px
    overflow: hidden
    font-weight: 200
    .menu-wrapper
      box-sizing: border-box
      flex: 0 0 80px
      width: 80px
      height: 100%
      background-color: #f3f5f7
      .menu-item
        display: flex
        flex-direction: row
        align-items: center
        justify-content: center
        height: 54px
        margin: 0 12px
        line-height: 14px
        border-bottom : 1px solid rgba(7,17,27,0.1)
        .name
          font-size: 12px
          color: #07111B
    .foods-wrapper
      flex: 1
</style>
