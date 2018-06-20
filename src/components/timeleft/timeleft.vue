<template>
<div class='progress-wrapper'>
    <progress :percent='percent' activeColor='#ea5a49' class='progress-bar'></progress>
    <p class='text'>{{getYear}}已经过去了{{days}}天,{{percent}}%</p>
</div>

</template>
<script>
    export default {
      data () {
        return {
          // year,
          // progress
        }
      },
      computed: {
        getYear () {
          return new Date().getFullYear()
        },
        days () {
          let start = new Date()
          start.setMonth(0)
          start.setDate(1)
        //   console.log(start)
          let offset = new Date().getTime() - start.getTime()
        //   console.log(offset)
          return parseInt(offset / 1000 / 60 / 60 / 24) + 1
        },
        isLeapYear () {
          const year = new Date().getFullYear()
          if (year % 400 === 0) {
            return true
          } else if (year % 4 === 0 && year % 100 !== 0) {
            return true
          } else {
            return false
          }
        },
        percent () {
          if (this.isLeapYear) {
            return parseInt(this.days * 100 / 366)
          } else {
            return parseInt(this.days * 100 / 365)
          }
        }
      }
    }
</script>
<style lang='stylus'>
.progress-wrapper
    margin-top 20px
    .progress-bar
        margin-bottom 10px
    .text
        text-align center
</style>
