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
          <icon :supportType="seller.supports[0].type" imgType="1"></icon>
          <span class="offers-text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" @click="showDetail" class="support-count">
        <span class="count-text">{{seller.supports.length}}个</span>
        <span class="arrow-icon"></span>
      </div>
    </div>
    <div @click="showDetail" class="bulletin-wrapper">
      <div class="brand"></div>
      <div class="title">{{seller.bulletin}}</div>
      <div class="arrow-icon"></div>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>

    <!--详情浮层-->
    <transition name="fade">
      <div v-show="isDetailShow" class="detail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>

            <!--星级-->
            <div class="star-wrapper">
              <star :score="seller.score" :size=48></star>
            </div>

            <!--标题-->
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>

            <!--活动详情-->
            <div v-if="seller.supports" class="supports">
              <div class="support-item" v-for="item in seller.supports">
                <span class="icon-wrapper">
                  <icon :supportType="item.type" imgType="2"></icon>
                </span>
                <span class="text">{{item.description}}</span>
              </div>
            </div>

            <!--标题-->
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>

            <!--公告详情-->
            <div class="bulletin">
              <p class="text">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="closeDetail"></div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">

  import star from 'components/star/star'
  import icon from 'components/icon/icon'

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        isDetailShow: false
      }
    },
    created () {

    },
    methods: {
      showDetail () {
        console.log('shows')
        this.isDetailShow = true
      },
      closeDetail () {
        this.isDetailShow = false
      }
    },
    components: {
      star,
      icon
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
          align-items: cente
          margin-top: 10px
          margin-bottom: 2px
          line-height: 12px

          /*.icon*/
          /*display: inline-block*/
          /*width: 12px*/
          /*height: 12px*/

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
      display: flex
      flex-direction: row
      align-items: center
      height: 28px
      padding: 0 12px
      background-color: rgba(7, 17, 27, 0.2)
      color: #fff
      .brand
        width: 22px
        height: 12px
        background-size: 22px 12px
        background-repeat: no-repeat
        bg-img('bulletin')
      .title
        flex: 1
        line-height: 28px
        font-size: 10px
        margin: 0 4px
        text-align: center
        text-overflow: ellipsis
        overflow: hidden
        white-space: nowrap
      .arrow-icon
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
    .fade-enter-active, .fade-leave-active
      transition: opacity 0.5s
    .fade-enter, .fade-leave-to
      opacity: 0
    .detail
      position: fixed
      left: 0
      top: 0
      z-index: 100
      width: 100%
      height: 100%
      overflow: auto
      background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height: 100%
        width: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
          color: #fff
          .name
            line-height: 16px
            font-size: 16px
            font-weight: 700
            text-align: center
          .star-wrapper
            margin-top: 18px
            padding: 2px 0
            text-align: center
          .title
            display: flex
            width: 80%
            margin: 28px auto 24px auto
            align-items: center
            .line
              flex: 1
              border-bottom: 1px solid rgba(255, 255, 255, 0.2)
            .text
              font-size: 14px
              padding: 0 12px
              font-weight: 700
          .supports
            display: flex
            flex-direction: column
            width: 80%
            margin: 0 auto
            .support-item
              display: flex
              flex-direction: row
              align-items: center
              padding: 0 12px
              margin-bottom: 12px
              font-size: 0
              &:last-child
                margin-bottom: 0
              .icon-wrapper
                margin-right : 6px
              .text
                font-size: 12px
          .bulletin
            width: 80%
            margin: 0 auto
            .text
              font-size: 12px
              padding: 0 12px
              line-height: 24px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        background-image: url("delete_white.png")
        background-size: 32px 32px
        clear: both


</style>
