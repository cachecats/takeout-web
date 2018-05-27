<template>
  <div class="shopcart">
    <div class="content" @click="toggleMask()">
      <div class="left-content">
        <div class="logo-wrapper">
          <div class="icon-wrapper" :class="{'highlight': totalCount>0}">
            <img :src='shopcartImg' class="icon"/>
          </div>
          <div class="count" v-show="totalCount > 0">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight': totalPrice>0}">¥{{totalPrice}}</div>
        <div class="vertical-line"></div>
        <div class="desc">另需配送费{{deliveryPrice}}元</div>
      </div>
      <div class="right-content" :class="descClass" @click.stop="checkOut">
        {{payDesc}}
      </div>
    </div>
    <div class="shopcart-list" v-if="showCartList">
      <div class="list-header">
        <span class="cart">购物车</span>
        <span class="clear" @click="clearCart">清空</span>
      </div>
      <div class="list-item" v-for="(item, index) in selectFoods">
        <span class="name">{{item.name}}</span>
        <span class="rmb">¥</span>
        <span class="price">{{item.price}}</span>
        <span>
          <cartcontrol :food="item"></cartcontrol>
        </span>
      </div>
    </div>
    <div class="mask" ref="mask" :hidden="!showCartList" @click="hideMask"></div>
  </div>
</template>

<script>

  import cartcontrol from '../cartcontrol/cartcontrol.vue'

  export default {
    props: {
      deliveryPrice: {
        type: Number
      },
      minPrice: {
        type: Number
      },
      selectFoods: {
        type: Array,
        default () {
          return []
        }
      },
    },

    data () {
      return {
        maskShow: false
      }
    },

    components: {
      cartcontrol
    },
    computed: {
      totalPrice () {
        let price = 0
        this.selectFoods.forEach((food) => {
          price += food.price * food.count
        })
        return price
      },
      totalCount () {
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })

        if(count === 0){
          this.maskShow = false
        }
        return count
      },
      shopcartImg () {
        let path = this.totalCount > 0 ? require('../../assets/img/shopcart_white.png') : require('../../assets/img/shopcart.png')
        return path
      },
      payDesc () {
        if (this.totalPrice === 0) {
          return `¥${this.minPrice}起送`
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差¥${diff}元起送`
        } else {
          return '去结算'
        }
      },
      descClass () {
        if (this.totalPrice >= this.minPrice) {
          return 'enough'
        } else {
          return 'not-enough'
        }
      },

      //判断是否显示购物车列表
      showCartList () {
        if (this.totalCount === 0) {
          return false
        }
        return this.maskShow
      },

    },

    created () {
      this.$nextTick(() => {
        let h = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight
        console.log('屏幕高度：' + h)
        this.$refs.mask.style.height = h + 'px'
      })
    },

    methods: {
      toggleMask () {
        if (this.totalCount !== 0) {
          this.maskShow = !this.maskShow
        }
      },
      hideMask(){
        this.maskShow = false
      },

      //清空购物车
      clearCart(){
        this.selectFoods.forEach((food) => {
          if(food.count){
            food.count = 0
          }
        })
      },

      //结账
      checkOut(){
        if (this.totalPrice >= this.minPrice) {
          window.alert("结账")
        }
      }
    },
  }

</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position: fixed
    left: 0
    bottom: 0
    width: 100%
    height: 48px
    z-index: 50
    background-color: #131d26
    box-sizing : border-box
    .content
      display: flex
      width: 100%
      height: 100%
      flex-direction: row
      font-size: 0
      .left-content
        flex: 1
        display: flex
        flex-direction: row
        .logo-wrapper
          position: relative
          display: flex
          align-items: center
          justify-content: center
          width: 56px
          height: 56px
          box-sizing: border-box
          top: -10px
          border-radius: 50%
          background: #131d26
          margin: 0 12px
          padding: 6px
          z-index: 70
          .count
            position: absolute
            top: 0
            right: 0
            width: 24px
            height: 16px
            line-height: 16px
            border-radius: 16px
            text-align: center
            font-size: 12px
            font-weight: 700
            background: rgb(240, 20, 20)
            color: #fff
            box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
          .icon-wrapper
            display: flex
            align-items: center
            justify-content: center
            width: 44px
            height: 44px
            border-radius: 50%
            background: #2b343c
            &.highlight
              background: #00A0DC
          .icon
            width: 25px
            height: 25px
        .price
          margin-right: 12px
          font-size: 16px
          color: #919396
          align-self: center
          font-weight: 700
          &.highlight
            color: #fff
        .vertical-line
          width: 1px
          height: 60%
          align-self: center
          background: rgba(255, 255, 255, 0.1)
        .desc
          margin-left: 12px
          align-self: center
          font-size: 12px
          font-weight: 500
          line-height: 24px
          color: rgba(255, 255, 255, 0.4)
      .right-content
        display: flex
        justify-content: center
        align-items: center
        width: 105px
        height: 100%
        background-color: #2b333b
        font-size: 12px
        font-weight: 700
        color: rgba(255, 255, 255, 0.4)
        &.not-enough
          background-color: #2b333b
        &.enough
          background: #00b43c
          color: #fff
    .shopcart-list
      position: absolute
      bottom: 48px
      z-index: 60
      display: flex
      flex-direction: column
      width: 100%
      height: 300px
      background: #fff
      font-weight : 200
      box-sizing : border-box
      .list-header
        display: flex
        width: 100%
        height: 40px
        line-height : 40px
        padding: 0 18px
        align-items : center
        justify-content: space-between
        box-sizing : border-box
        background: #f3f5f7
        border-bottom : 1px solid rgba(7,17,27,0.1)
        .cart
          color: rgb(7,17,27)
          font-size : 14px
          line-height : 40px
        .clear
          color: rgb(0,160,220)
          font-size : 12px
          line-height : 40px
      .list-item
        display: flex
        align-items : center
        height: 48px
        line-height : 48px
        margin: 0 18px
        box-sizing : border-box
        white-space : nowrap
        overflow-x : hidden
        border-bottom : solid 1px rgba(7,17,27,0.1)
        .name
          flex: 1
          font-size : 14px
          line-height : 24px
          color: rgb(7,17,27)
        .rmb
          font-size : 10px
          color: rgb(240,20,20)
          font-weight : normal
          line-height : 24px
        .price
          font-size : 12px
          color: rgb(240,20,20)
          font-weight : 700
          line-height : 24px
    .mask
      position: absolute
      bottom: 48px
      width: 100%
      z-index: 55
      background: rgba(0, 0, 0, 0.4)
</style>
