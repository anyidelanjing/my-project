<template>
  <div>
    <Card v-for='book in books' :key='book.id' :book='book'></Card>
    <p class="text-footer" v-if='!more'>没有更多数据</p>
  </div>
</template>

<script>
import {get} from '@/utils'
import Card from '@/components/Card/Card'
export default {
  components: {Card},
  data () {
    return {
       books: [],
       page: 0,
       more: true
    }
  },
  methods: {
    async getBooks(init) {
       if (init) {
         this.page = 0;
         this.more = true;
       }
       wx.showNavigationBarLoading()
       const books = await get('/weapp/booklist',{page: this.page})
       
       if (books.list.length <10 && this.page >0) {
         this.more = false
       }
       if (init) {
         this.books = books.list
       } else {
         this.books = this.books.concat(books.list)
       }
       wx.stopPullDownRefresh()
       wx.hideNavigationBarLoading()
    }
  },
  onPullDownRefresh() {
    this.getBooks(true)
    // console.log('下拉')
  },
  onReachBottom() {
    if(!this.more) {
      return false
    }
    this.page = this.page + 1
    this.getBooks()
  },
  mounted () {
    this.getBooks(true)
  }
}
// Use Vuex
</script>

<style>
  .text-footer {
    text-align: center;
    font-size: 12px;
    margin-bottom: 5px;
  }
</style>
