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
      <div class="right-content" :class="descClass">
        {{payDesc}}
      </div>
    </div>
    <div class="shopcart-list" v-if="showCartList">
      <div class="list-header">
        <span class="cart">购物车</span>
        <span class="clear">清空</span>
      </div>
      <div class="list-content">列表内容</div>
    </div>
  </div>
</template>

<script>
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
        default(){
          return []
        }
      },
    },

    data(){
      return {
        maskShow: false
      }
    },

    components: {},
    computed: {
      totalPrice(){
        let price = 0
        this.selectFoods.forEach((food) => {
          price += food.price * food.count
        })
        return price
      },
      totalCount(){
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      },
      shopcartImg(){
        let path = this.totalCount > 0 ? require("../../assets/img/shopcart_white.png") : require("../../assets/img/shopcart.png")
        return path
      },
      payDesc(){
        if (this.totalPrice === 0) {
          return `¥${this.minPrice}起送`
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差¥${diff}元起送`
        } else {
          return '去结算'
        }
      },
      descClass(){
        if (this.totalPrice >= this.minPrice) {
          return 'enough'
        } else {
          return 'not-enough'
        }
      },

      //判断是否显示购物车列表
      showCartList(){
        if(this.totalCount === 0){
          return false
        }
        return this.maskShow
      }

    },

    created(){

    },

    methods: {
      toggleMask(){
        this.maskShow = !this.maskShow
        console.log(this.maskShow)
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
      width: 100%
      z-index: 60
</style>
