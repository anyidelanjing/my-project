<template>
    <div class="rate">
        <span>☆☆☆☆☆</span> 
         <div class="hollow" :style='style'>★★★★★</div>
    </div>
</template>
<script type='text/ecmascript-6'>
    export default {
        props: {
            value: {
                type: Number,
                default: 0
            }
        },
        computed: {
            style() {
                return `width:${(this.value)/2-0.17*this.value/2}em`
            }
        }
    }
</script>
<style lang='stylus' rel='stylesheet/stylus'>
    .rate
        position relative
        display inline-block
        color: #ea5149
        font-size: 14px;
        .hollow
            position absolute
            display inline-block
            top 0
            left 0
            width 0
            overflow hidden

</style>