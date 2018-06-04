<template>
  <transition name="move">
    <div class="food" ref="food" v-show="showFlag">
      <div class="food-detail">
        <div class="image-header">
          <img :src="food.image"/>
          <div class="back" @click="goBack">
            <i class="icon-arrow_lift"></i>
          </div>
        </div>
        <div class="content-wrapper">
          <div class="name">{{food.name}}</div>
          <div class="sell-wrapper">
            <span class="sell-count">{{"月售" + food.sellCount + "份"}}</span>
            <span class="rating">{{"好评率" + food.rating + "%"}}</span>
          </div>
          <div class="bottom-wrapper">
            <div class="price-wrapper">
              <div class="price-now-wrapper">
                <span class="rmb">¥</span>
                <span class="current-price">{{food.price}}</span>
              </div>
              <div class="price-old-wrapper" v-show="food.oldPrice">
                <span class="rmb">¥</span>
                <span class="old-price">{{food.oldPrice}}</span>
              </div>
            </div>
            <transition name="fade">
              <div class="add-cart" v-show="!food.count || food.count == 0" @click="addToCart">加入购物车</div>
            </transition>
            <div class="cart-controll-wrapper">
              <cartcontrol :food="food" v-show="food.count || food.count > 0"></cartcontrol>
            </div>
          </div>
        </div>
        <split v-show="food.info"></split>
        <div class="info-wrapper" v-show="food.info">
          <div class="title">商品介绍</div>
          <div class="info">{{food.info}}</div>
        </div>
        <split></split>
        <div class="rating">
          <div class="title">商品评价</div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script type="text/ecmascript-6">

  import Vue from 'vue'
  import cartcontrol from 'components/cartcontrol/cartcontrol'
  import split from 'components/split/split'
  import BScroll from 'better-scroll'

  export default {
    props: {
      food: {
        type: Object
      }
    },
    components: {
      cartcontrol,
      split
    },
    data () {
      return {
        showFlag: false
      }
    },
    created () {

    },
    methods: {
      showFood () {
        this.showFlag = true
        //注意：better-scroll 必须只有一个子元素
        //在组件显示时初始化
        this.$nextTick(() => {
          //因为可能会多次显示隐藏，加判断防止重复初始化
          if (!this.scroll) {
            this.scroll = new BScroll(this.$refs.food, {
              click: true
            })
          } else {
            this.scroll.refresh()
          }
        })
      },

      //返回
      goBack () {
        this.showFlag = false
      },

      //添加到购物车
      addToCart(){
        Vue.set(this.food, "count", 1)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

  .move-enter-active, .move-leave-active
    transition: all .2s linear
    transform: translate3d(0, 0, 0)

  .move-enter, .move-leave-to
    transform: translate3d(100%, 0, 0)

  .food
    position: fixed
    left: 0
    top: 0
    bottom: 48px
    width: 100%
    background-color: white
    z-index: 30
    .image-header
      position: relative
      width: 100%
      height: 0
      padding-top: 100%
      img
        position: absolute
        left: 0
        top: 0
        width: 100%
        height: 100%
      .back
        position: absolute
        top: 10px
        left: 0
        padding: 10px
        .icon-arrow_lift
          font-size: 14px
          color: #fff
    .content-wrapper
      display: flex
      flex-direction: column
      width: 100%
      padding: 18px
      box-sizing: border-box
      .name
        font-size: 14px
        line-height: 14px
        color: rgb(7, 17, 27)
        font-weight: 700
      .sell-wrapper
        display: flex
        flex-direction: row
        padding-top: 8px
        .sell-count, .rating
          font-size: 10px
          color: rgb(147, 153, 159)
          line-height: 10px
          margin-right: 12px
      .bottom-wrapper
        position: relative
        display: flex
        flex-direction: row
        align-items: center
        margin-top: 18px
        box-sizing: border-box
        .price-wrapper
          display: flex
          align-items: center
          .price-now-wrapper
            display: flex
            align-items: baseline
            .rmb
              color: rgb(240, 20, 20)
              font-size: 10px
              line-height: 24px
            .current-price
              color: rgb(240, 20, 20)
              font-size: 14px
              font-weight: 700
              line-height: 24px
          .price-old-wrapper
            display: flex
            align-items: baseline
            margin-left: 12px
            text-decoration: line-through
            .rmb
              color: rgb(147, 153, 159)
              font-size: 10px
              line-height: 24px
            .old-price
              color: rgb(147, 153, 159)
              font-size: 10px
              font-weight: 700
              line-height: 24px
        .fade-enter-active, .fade-leave-active
          transition: all 0.2s
          opacity: 1
        .fade-enter, .fade-leave-to
          opacity: 0
        .add-cart
          position: absolute
          right: 0
          font-size: 10px
          color: #fff
          text-align: center
          border-radius: 12px
          background-color: rgb(0, 160, 200)
          padding: 6px 12px
        .cart-controll-wrapper
          position: absolute
          right: 0px

    .info-wrapper
      padding: 18px
      .title
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
      .info
        font-size: 12px
        color: rgb(77, 85, 93)
        line-height: 24px
        padding: 8px
    .rating
      margin-top : 18px
      .title
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
        padding-left : 18px

</style>
