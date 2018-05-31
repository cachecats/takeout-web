<template>
  <view class="food-detail">
    <span>{{food.name}}</span>
  </view>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      food: {
        type: Object
      }
    },
    data () {
      return {
        showFlag: true
      }
    },
    created () {

    },
    methods: {
      showFood () {
        this.showFlag = true
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .food-detail
    position: fixed
    left: 0
    bottom: 0
    width: 100%
    background-color: red
    z-index: 80

</style>
