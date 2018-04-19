<template>
  <div class="header-div">
    <div class="content-wrapper">
      <img width="64" height="64" :src="seller.avatar" style="border-radius: 2px">
      <div class="shop-info">
        <div class="shop-name">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="delivery">
          <span>{{seller.description}}/{{seller.deliveryTime}}分钟送达</span>
        </div>
        <div v-if="seller.supports" class="offers">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="offers-text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count-text">{{seller.supports.length}}个</span>
        <span class="arrow-icon"></span>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="brand"></span>
      <span class="title">{{seller.bulletin}}</span>
      <span class="arrow-icon"></span>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    created(){
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

  @import "../../common/stylus/mixin"

  .header-div
    position: relative
    overflow: hidden
    background-color: rgba(7, 17, 27, 0.5)
    font-weight: 200
    .content-wrapper
      display: flex
      position: relative
      flex-direction: row
      padding: 24px 12px 18px 24px
      font-size: 0
      .shop-info
        display: flex
        flex-direction: column
        margin-left: 16px
        color: rgb(255, 255, 255)
        .shop-name
          margin-top: 2px
          display: flex
          flex-direction: row
          align-items: center
          .brand
            display: inline-block
            width: 30px
            height: 18px
            bg-img('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            font-weight: bold
        .delivery
          font-size: 12px
          line-height: 12px
          margin-top: 8px
        .offers
          display: flex
          flex-direction: row
          align-items: center
          margin-top: 10px
          margin-bottom: 2px
          line-height: 12px
          .icon
            display: inline-block
            width: 12px
            height: 12px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-img('decrease_1')
            &.discount
              bg-img('discount_1')
            &.special
              bg-img('special_1')
            &.invoice
              bg-img('invoice_1')
            &.guarantee
              bg-img('guarantee_1')
          .offers-text
            margin-left: 4px
            font-size: 10px
            text-align: center
      .support-count
        display: flex
        flex-direction: row
        position: absolute
        justify-content: center
        align-items: center
        right: 12px
        bottom: 14px
        background-color: rgba(0, 0, 0, 0.2)
        border-radius: 14px
        padding: 0 8px
        height: 24px
        .count-text
          font-size: 10px
          line-height: 12px
          color: #fff
        .arrow-icon
          width: 12px
          height: 12px
          background-image: url("arrow.png")
          background-size: 12px 12px
          background-repeat: no-repeat
          margin-left: 2px
    .bulletin-wrapper
      position: relative
      align-items: center
      height: 28px
      line-height: 28px
      padding: 0 12px
      background-color: rgba(7, 17, 27, 0.2)
      text-overflow: ellipsis
      overflow: hidden
      white-space: nowrap
      color: #fff
      .brand
        display: inline-block
        vertical-align: top
        width: 22px
        height: 12px
        margin-top: 8px
        background-size: 22px 12px
        background-repeat: no-repeat
        bg-img('bulletin')
      .title
        vertical-align: top
        font-size: 10px
        margin: 0 4px 0 0
      .arrow-icon
        position: absolute
        right: 10px
        bottom: 8px
        width: 12px
        height: 12px
        background-image: url("arrow.png")
        background-size: 12px 12px
        background-repeat: no-repeat
    .background
      position: absolute
      left: 0
      top: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
</style>
