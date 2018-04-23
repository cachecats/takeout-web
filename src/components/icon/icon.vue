<!--活动的icon图标组件-->

<template>
  <div :class="imgTypeClass">
    <span class="icon" :class="classMap[supportType]"></span>
  </div>

</template>

<script>
  export default {
    props: {
      supportType: { //活动类型
        type: Number
      },
      imgType: { //图片类型.可选值：img1,img2,img3,img4分别对应1,2,3,4四种小icon图标
        type: String
      },
    },
    computed: {
      imgTypeClass(){
        return 'img' + this.imgType
      }
    },
    created(){
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  }

</script>

<style lang="stylus" rel="stylesheet/stylus">

  @import "../../common/stylus/mixin"
  .img1
    display: inline-block
    width: 12px
    height: 12px
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

  .img2
    display: inline-block
    width: 16px
    height: 16px
    .icon
      display: inline-block
      width: 16px
      height: 16px
      background-size: 16px 16px
      background-repeat: no-repeat
      &.decrease
        bg-img('decrease_2')
      &.discount
        bg-img('discount_2')
      &.special
        bg-img('special_2')
      &.invoice
        bg-img('invoice_2')
      &.guarantee
        bg-img('guarantee_2')

  .img3
    display: inline-block
    width: 12px
    height: 12px
    .icon
      display: inline-block
      width: 12px
      height: 12px
      background-size: 12px 12px
      background-repeat: no-repeat
      &.decrease
        bg-img('decrease_3')
      &.discount
        bg-img('discount_3')
      &.special
        bg-img('special_3')
      &.invoice
        bg-img('invoice_3')
      &.guarantee
        bg-img('guarantee_3')

  .img4
    display: inline-block
    width: 12px
    height: 12px
    .icon
      display: inline-block
      width: 12px
      height: 12px
      background-size: 12px 12px
      background-repeat: no-repeat
      &.decrease
        bg-img('decrease_4')
      &.discount
        bg-img('discount_4')
      &.special
        bg-img('special_4')
      &.invoice
        bg-img('invoice_4')
      &.guarantee
        bg-img('guarantee_4')
</style>
