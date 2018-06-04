<template>
  <div class="rating-select">
    <div class="label-wrapper">
      <span class="label positive" :class="{active: selectType === 0}" @click="chooseType(0)">{{desc.all}}<span class="num">47</span></span>
      <span class="label positive" :class="{active: selectType === 1}" @click="chooseType(1)">{{desc.positive}}<span
        class="num">40</span></span>
      <span class="label negative" :class="{active: selectType === 2}" @click="chooseType(2)">{{desc.negative}}<span
        class="num">7</span></span>
    </div>
    <div class="content">
      <i class="icon-check_circle" :class="{active: onlyContent}" @click="toggleCheck"></i>
      <span class="text">只看有内容的评价</span>
    </div>
  </div>
</template>

<script>

  const ALL = 0;
  const POSITIVE = 1;
  const NEGATIVE = 2;

  export default {
    props: {
      ratings: {
        type: Array,
        default(){
          return []
        }
      },
      selectType: {
        type: Number,
        default: ALL
      },
      onlyContent: {
        type: Boolean,
        default: true
      },
      desc: {
        type: Object,
        default(){
          return {
            all: '全部',
            positive: '推荐',
            negative: '差评'
          }
        }
      }
    },
    components: {},
    methods: {
      //切换check的状态
      toggleCheck(){
        this.$emit("toggleCheck")
      },
      //选择类型
      chooseType(type){
        this.$emit("chooseType", type)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .rating-select
    margin-top: 18px
    .label-wrapper
      margin: 0 18px
      padding-bottom: 18px
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      font-size: 0
      .label
        font-size: 12px
        line-height: 16px
        border-radius: 2px
        padding: 8px 12px
        color: rgb(77, 85, 93)
        margin-right: 8px
        &.positive
          background-color: rgba(0, 160, 220, 0.2)
          &.active
            background-color: rgb(0, 160, 220)
            color: #fff
        &.negative
          background-color: rgba(77, 85, 93, 0.2)
          &.active
            background-color: rgb(77, 85, 93)
            color: #fff
        .num
          font-size: 8px
          margin-left: 3px
    .content
      display: flex
      align-items: center
      padding: 12px 18px
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      .icon-check_circle
        font-size: 24px
        line-height: 24px
        color: rgb(147, 153, 159)
        &.active
          color: #00c850
      .text
        font-size: 12px
        line-height: 24px
        color: rgb(147, 153, 159)
        margin-left: 4px
</style>
