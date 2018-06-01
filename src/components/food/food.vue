<template>
  <transition name="move">
    <div class="food-detail" v-if="showFlag">
      <div class="image-header">
        <img :src="food.image"/>
        <div class="back" @click="goBack">
          <i class="icon-arrow_lift"></i>
        </div>

      </div>

    </div>

  </transition>
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
        showFlag: false
      }
    },
    created () {

    },
    methods: {
      showFood () {
        this.showFlag = true
      },
      goBack(){
          this.showFlag = false
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
  .food-detail
    position: fixed
    left: 0
    top: 0
    width: 100%
    height: 100%
    background-color: white
    z-index: 30
    .image-header
      position: relative
      width:100%
      height: 0
      padding-top : 100%
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
          font-size : 14px
          color: #fff



</style>
