<template>
  <div class="star" :class="starType">
    <span class="star-item" :class="itemClass" v-for="item in items"></span>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      star: { //评分
        type: Number
      },
      size: { //大小
        type: Number
      }
    },
    data () {
      return {}
    },
    created () {

    },
    computed: {

    },
    methods: {}
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

</style>
