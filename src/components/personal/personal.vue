<template>
  <div class='wrapper-info'>
    <div class='user'>
        <open-data type="userAvatarUrl" class='avatar'></open-data>
        <open-data type="userNickName" class='name'></open-data>
    </div>
    <div class='timer'>
      <timeleft></timeleft>
      <!-- 123 -->
    </div>
    <button class='btn'  @click="scanBook">添加图书</button>
  </div>
</template>

<script>
import timeleft from '../../components/timeleft/timeleft'
export default {
  data () {
    return {
      // active: true
    }
  },
  methods: {
    scanBook () {
      // console.log(1)
      wx.scanCode({
        success: (res) => {
          console.log(res)
        }
      })
    }
  },
  components: {timeleft}
}
</script>

<style lang='stylus'>
.wrapper-info
  display flex
  flex-direction column
  align-items  center
  box-sizing border-box
  padding 10%
  width 100%
  height 100%
  .user
    margin-top 100rpx
    text-align center
    .avatar
      display block
      overflow hidden
      margin-bottom 30rpx
      width 150rpx
      height 150rpx
      border-radius 50%
  .timer
    margin-top 20px
    width 100%
  .btn
    color white
    background #ea5a49
    margin-top 60px
    width 100%
    border-radius 2px
    font-size 16px
  .button-hover
    background: #fa5a49
      


</style>
