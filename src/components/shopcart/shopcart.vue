<template>
  <div class="shopcart">
    <div class="content">
      <div class="left-content">
        <div class="logo-wrapper">
          <div class="icon-wrapper">
            <img src="../../assets/img/shopcart.png" class="icon"/>
          </div>
        </div>
        <div class="price">¥0</div>
        <div class="vertical-line"></div>
        <div class="desc">另需配送费4元</div>
      </div>
      <div class="right-content">
        <span class="right-text">¥ 20起送</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {

    components: {},
    data(){
      return {}
    },

    created(){

    },

    methods: {},
    computed: {}
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
      font-size : 0
      .left-content
        flex: 1
        display: flex
        flex-direction : row
        .logo-wrapper
          position: relative
          display: flex
          align-items: center
          justify-content : center
          width: 56px
          height: 56px
          box-sizing : border-box
          top: -10px
          border-radius : 50%
          background: #131d26
          margin: 0 12px
          padding: 6px
          .icon-wrapper
            display: flex
            align-items: center
            justify-content : center
            width: 44px
            height: 44px
            border-radius : 50%
            background: #2b343c
          .icon
            width: 25px
            height: 25px
        .price
          margin-right : 12px
          font-size : 16px
          color: #919396
          align-self :center
          font-weight : 700
        .vertical-line
          width: 1px
          height: 60%
          align-self : center
          background: rgba(255,255,255,0.1)
        .desc
          margin-left : 12px
          align-self : center
          font-size : 12px
          font-weight : 500
          line-height : 24px
          color: rgba(255,255,255,0.4)
      .right-content
        display: flex
        justify-content: center
        align-items : center
        width: 105px
        height: 100%
        background-color: #2b333b
        .right-text
          font-size : 12px
          font-weight : 700
          color: rgba(255,255,255,0.4)

</style>
