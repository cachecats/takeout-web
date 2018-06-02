<template>
  <div class="wrapper">
    <div class="cart-decrease icon-remove_circle_outline" v-if="food.count>0" @click.stop.prevent="decreaseCount"></div>
    <div class="cart-count" v-if="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCount"></div>
  </div>

</template>

<script type="text/ecmascript-6">

  import Vue from 'vue'

  export default {
    props: {
      food:{
        type: Object
      }
    },
    data () {
      return {}
    },
    created () {
//      console.log(this.food)
    },
    methods: {
      addCount(){
        if (!this.food.count){
          Vue.set(this.food, 'count', 1)
        }else{
          this.food.count ++
        }

        console.log(this.food.count)
      },
      decreaseCount(){
        this.food.count --
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

  .wrapper
    font-size: 0
    display: flex
    align-items : center
    .cart-decrease, .cart-add
      display: inline-block
      font-size : 24px
      color: rgb(0,160,220)
      line-height : 24px
      padding: 6px
    .cart-count
      font-size : 10px
      line-height: 24px
      color: rgb(147,153,159)

</style>
