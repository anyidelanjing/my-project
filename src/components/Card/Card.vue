<template>
  <div class="book-card" >
      <div class="thumb">
          <img :src="book.image" alt="" class='img' mode='aspectFit'>
      </div>
      <div class="detail">
          <div class="row">
              <div class="right">
                  {{book.rate}} <star :value='book.rate'></star>
              </div>
              <div class="left">
                  {{book.title}}
              </div>
          </div>
           <div class="row">
              <div class="right">
                   浏览量：
              </div>
              <div class="left">
                  {{book.author}}
              </div>
          </div>
           <div class="row">
              <div class="right">
                  添加人：
              </div>
              <div class="left">
                  {{book.publisher}}
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import star from '@/components/star/star'
    export default {
        // created() {
        //     console.log(book)
        // },
        props:{
            book:{
                type: Object
            }
        },
        components:{star}
    }
</script>
<style lang='stylus' rel='stylesheet/stylus' >
    .book-card
        padding: 5px
        overflow: hidden
        margin-top 5px
        margin-bottom 5px
        font-size 14px
        .thumb
            width: 90px
            height 90px
            float left 
            margin: 0 auto
            overflow hidden
            .img
                max-width 100%
                max-height 100%
        .detail
            margin-left 100px
            .row
                line-height 20px
                margin-bottom 3px
                // color: #ea5149
                .right
                    float: right
                .left
                    margin-right 80px    

</style>