<template>
    <div class='wrapper'>
      <div class='unlogin-wrapper' v-if='!userinfo'>
         <div class='img-wrapper'>
           <img src="/static/img/unlogin-48.png" alt="" width='60' height='60'>
         </div>
         <div class='userinfo-wrapper'>
           <button open-type='getUserInfo' @getuserinfo='onGotUserInfo'>点击登录</button>
         </div>
         <!-- <div v-if='showAlert' class='sucLogin'>登录成功!</div> -->
      </div>
      <div class='login-wrapper' v-if='showAlert'>
        <div class='user'>
          <open-data type="userAvatarUrl" class='avatar'></open-data>
          <open-data type="userNickName" class='name'></open-data>
        </div>
      </div>
      <!-- <div class='personal-wrapper' v-if='showAlert'>
          <personal ></personal>
      </div>  -->
      <div class='timer' style='width: 80%'>
        <timeleft></timeleft>
      </div>
      <button v-if='showAlert' class='btn'  @click="scanBook">添加图书</button>
    </div>   
</template>

<script>
// import personal from '../../components/personal/personal'
import timeleft from '../../components/timeleft/timeleft'
// import config from '../../config'
export default {
  data () {
    return {
      toggleshow: true,
      userinfo: false
    }
  },
  created () {

  },
  computed: {
    showPersonal (e) {
      this.toggleshow = !this.toggleshow
      console.log(this.toggleshow)
    },
    showAlert () {
      return this.userinfo
    }
  },
  methods: {
    onGotUserInfo (e) {
      if (e.target.userInfo) {
        this.userinfo = true
      }
      console.log('登录成功')
      //  console.log(e)
    // console.log(e.mp.detail.rawData)
    },
    scanBook () {
      wx.scanCode({
        success: (res) => {
          console.log(res)
        }
      })
    }
  },
  components: {
    timeleft
  }

}
</script>

<style lang='stylus'>
.wrapper
    position fixed
    top 0
    left 0
    width 100%
    height 100%
    display flex
    flex-direction column
    align-items center
    justify-content center
    .unlogin-wrapper
      width 80%
      .img-wrapper
        margin:0 auto
        width 64px
        height 64px
        overflow hidden
        img
          display inline-block
          width 64px
          height 64px
      .userinfo-wrapper
        margin 20px auto 0
        width: 160px
        margin-top:20px;
        button
          line-height 40px
          height 40px
          font-size:16px
          color grey
  .login-wrapper
    text-align center
    .avatar
      display block
      overflow hidden
      width 64px
      height 64px
      border-radius 50%
    .name
      margin 20px 0
  .btn
    margin-top 40px
    width:80%;
    font-size:16px;
    background-color:#EA5149;
    color:white;
    &.button-hover
      background: #fa5a49

    

          // background #ea5149

        // margin-top 40px
      // .sucLogin
      //   line-height 60rpx
      //   width 160rpx
      //   height 60rpx
      //   text-align center
      //   font-size 20rpx
      //   color white
      //   background grey
        // transition: all 0.5s ease
        // &.fade-enter,&.fade-leave-to
        //   opacity: 0
  // .personal-wrapper
  //   // z-index: 100
  //   position fixed
  //   top 0
  //   left 0
  //   width 100%
  //   height: 100%
  //     // background #fff   
</style>
