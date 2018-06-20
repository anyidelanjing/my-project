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
import config from '../../config'
import {post,showModal} from '@/utils/index.js'
// const {mysql} = require('/server/qcloud')
import qcloud from 'wafer2-client-sdk'
export default {
  data () {
    return {
      toggleshow: true,
      userinfo: false,
      openid: ''
    }
  },
  created () {
    console.log(qcloud.login)
  },
  computed: {
    showPersonal (e) {
      this.toggleshow = !this.toggleshow
      // console.log(this.toggleshow)
    },
    showAlert () {
      return this.userinfo
    }
  },
  methods: {
    onGotUserInfo (e) {
      if (e.target.userInfo) {
        this.userinfo = true
        let that = this
       wx.login({ 
        success: function(res) {
         let APPID = 'wx982d1b90336d0f2c';
         let  SECRET = 'b63eb135f3393bb0c88229d96404c485';
        // console.log(res.code)
        if (res.code) {
          //发起网络请求
          wx.request({
            url: 'https://api.weixin.qq.com/sns/jscode2session?appid='+APPID+'&secret='+SECRET+'&js_code='+res.code+'&grant_type=authorization_code',
            data: {
              code: res.code
            },
            success: function(res){
              // console.log(res.data.openid) 获取到openid
              console.log(res) //获取到openid
              //  mysql('csessioninfo').insert({'open_id': res.data.openid})
              that.openid = res.data.openid

            }
          })
        } else {
          console.log('登录失败！' + res.errMsg)
        }
      }
    });
// wx.login({
//   //      let APPID = 'wx982d1b90336d0f2c';
//     //      let  SECRET = 'b63eb135f3393bb0c88229d96404c485';
//         success: function (loginResult) {
//          let APPID = 'wx982d1b90336d0f2c';
//          let  SECRET = 'b63eb135f3393bb0c88229d96404c485';
//           var loginParams = {
//             code: loginResult.code,
//             encryptedData: e.target.encryptedData,
//             iv: e.target.iv,
//           }
//           qcloud.setLoginUrl('https://api.weixin.qq.com/sns/jscode2session?appid='+APPID+'&secret='+SECRET+'&js_code='+loginResult.code+'&grant_type=authorization_code')
//           qcloud.requestLogin({
//             loginParams,
//             success() {
//               // util.showSuccess('登录成功');

//               that.setData({
//                 userInfo: e.target.userInfo,
//                 logged: true
//               })
//             },
//             fail(error) {
//               // showModel('登录失败', error)
//               console.log('登录失败2', error)
//             }
//           });
//         },
//         fail: function (loginError) {
//           // showModel('登录失败', loginError)
//           console.log('登录失败1', loginError)
//         },
//       });
      }
      // console.log('登录成功')
       console.log(e)

    // console.log(e.mp.detail.rawData)
    },

    async addBook (isbn) {
      const res = await post('/weapp/addbook',{
        isbn,
        openid: this.openid
        })
        console.log(res)
        showModal('添加成功', res.title+'添加成功')
      // if (res.code ===0 &&res.data.title) {
      //   console.log(res.data.title+'添加成功')
      // }
    },
    scanBook () {
      wx.scanCode({
        success: (res) => {
          if (res.result) {
            // console.log(res.result)
            this.addBook(res.result)
          }
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
