<template>
  <div class="goods">
    <!--左侧菜单列表-->
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="icon-wrapper">
            <icon v-if="item.type>=0" :supportType="item.type" imgType="3"></icon>
          </span>
          <span class="name">{{item.name}}</span>
        </li>
      </ul>
    </div>
    <!--右侧商品列表-->
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul>
        <li v-for="item in goods" class="goods-item">
          <div class="title">{{item.name}}</div>
          <ul>
            <li v-for="food in item.foods" class="foods-item">
              <img :src="food.icon" width="57" height="57" class="icon">
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <div v-if="food.description" class="description">{{food.description}}</div>
                <div class="sales-rating">
                  <span class="sales">月售{{food.sellCount}}</span>
                  <span class="rating">好评率{{food.rating}}%</span>
                </div>
                <div class="price-wrapper">
                  <span class="rmb">¥</span>
                  <span class="price">{{food.price}}</span>
                  <span v-if="food.oldPrice" class="old-rmb">¥</span>
                  <span v-if="food.oldPrice" class="old-price">{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  import icon from 'components/icon/icon'
  import BScroll from 'better-scroll'
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
    components: {
      icon
    },
    created(){
      this.$http.get('static/data.json').then((res) => {
        this.goods = res.body.goods;
        this.$nextTick(() => {
          this.initBetterScroll();
        })
      })
    },
    methods: {
      initBetterScroll(){
        console.log("initBetterScroll")
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {});
        this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {});
      }
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
        height: 54px
        width: 56px
        margin: 0 12px
        line-height: 14px
        border-bottom: 1px solid rgba(7, 17, 27, 0.1)
        .name
          width: 56px
          font-size: 12px
          color: #07111B
        .icon-wrapper
          margin-right: 2px
    .foods-wrapper
      flex: 1
      font-size: 0
      .goods-item
        display: flex
        flex-direction: column
        .title
          height: 26px
          line-height: 26px
          background: #f3f5f7
          font-size: 12px
          color: rgb(147, 153, 159)
          padding-left: 14px
          border-left: 2px solid #d9dde1
        .foods-item
          display: flex
          flex-direction: row
          margin: 0 18px
          padding: 18px 0
          border-bottom: 1px solid rgba(7, 17, 27, 0.1)
          &.last-child
            border-bottom: 0 solid rgba(7, 17, 27, 0.1)
          .icon
            margin-right: 10px
          .content
            display: flex
            flex-direction: column
            flex: 1
            .name
              font-size: 14px
              line-height: 14px
              margin: 2px 0 8px 0
              color: #000
              font-weight: 500
            .description
              font-size: 10px
              color: rgb(147, 153, 159)
              line-height: 12px
              margin-bottom: 8px
            .sales-rating
              display: flex
              flex-direction: row
              font-size: 10px
              color: rgb(147, 153, 159)
              line-height: 10px
              .sales
                display: inline-block
                margin-right: 12px
              .rating
                display: inline-block
            .price-wrapper
              display: flex
              flex-direction: row
              line-height: 24px
              align-items baseline
              .rmb
                font-size: 10px
                color: red
                font-weight: normal
              .price
                font-size: 14px
                color: red
                font-weight: 700
                margin-right: 8px
              .old-rmb
                font-size: 10px
                color: rgb(147, 153, 159)
                font-weight: normal
                text-decoration : line-through
              .old-price
                font-size: 10px
                color: rgb(147, 153, 159)
                font-weight: 700
                text-decoration : line-through


</style>
