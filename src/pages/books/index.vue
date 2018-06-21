<template>
  <div>
    <Card v-for='book in books' :key='book.id' :book='book'></Card>
  </div>
</template>

<script>
import {get} from '@/utils'
import Card from '@/components/Card/Card'
export default {
  components: {Card},
  data () {
    return {
       books: []
    }
  },
  methods: {
    async getBooks() {
       const books = await get('/weapp/booklist')
        this.books = books.list
    }
  },
  created () {
    this.getBooks()
  }
}
// Use Vuex
</script>

<style>
</style>
