<template>
  <div>
    <div v-for='book in books' :key='book.id'>{{book.title}}</div>
  </div>
</template>

<script>
import {get} from '@/utils'
export default {
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
