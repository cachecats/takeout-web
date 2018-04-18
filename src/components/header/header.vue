<template>
  <div class="header">
    <img width="60" height="60" :src="seller.avatar" alt="">
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {
        type: Object
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

</style>
