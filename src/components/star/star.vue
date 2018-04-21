<template>
  <div class="star" :class="starType">
    <span class="star-item" :class="itemClass" v-for="itemClass in itemClasses"></span>
  </div>
</template>

<script type="text/ecmascript-6">

  const LENGTH = 5
  const CLS_ON = 'on' //一颗星
  const CLS_OFF = 'off' //没有星
  const CLS_HALF = 'half' //半颗星

  export default {
    props: {
      score: { //评分
        type: Number
      },
      size: { //大小
        type: Number
      }
    },
    data () {
      return {
        itemsClasses: []
      }
    },
    created () {

    },
    computed: {
      starType () {
        return 'star-' + this.size
      },
      itemClasses () {

        //存放结果的数组
        let result = []
        //格式化后的分数
        let score = Math.floor(this.score * 2) / 2
        //是否有小数
        let hasDecimal = (score % 1 !== 0)
        //满星的有几个
        let integer = Math.floor(score)

        //循环，有几颗满星的就在数组中放几个满星的class
        for (let i = 0; i < integer; i++) {
          result.push(CLS_ON)
        }
        //如果有半星接着补一个半星
        if (hasDecimal) {
          result.push(CLS_HALF)
        }
        //如果数组长度没有达到固定的长度，接着用没星补齐
        while (result.length < LENGTH) {
          result.push(CLS_OFF)
        }

        return result

      }

    },
    methods: {}
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .star
    font-size: 0
    .star-item
      display: inline-block
      background-repeat: no-repeat
    &.star-48
      .star-item
        width: 20px;
        height: 20px;
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0
        &.on
          bg-img('star48_on')
        &.off
          bg-img('star48_off')
        &.half
          bg-img('star48_half')
    &.star-36
      .star-item
        width: 15px;
        height: 15px;
        margin-right: 16px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-img('star36_on')
        &.off
          bg-img('star36_off')
        &.half
          bg-img('star36_half')
    &.star-24
      .star-item
        width: 10px;
        height: 10px;
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-img('star24_on')
        &.off
          bg-img('star24_off')
        &.half
          bg-img('star24_half')

</style>
