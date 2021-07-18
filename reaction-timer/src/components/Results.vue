<template>
<div>
  <p>Reaction Time - {{score}} ms </p>
  <p>{{rank}}</p>
</div>
</template>

<script>
export default {
    props: ['score'],
    data(){
        return {
            rank: null
        }
    },
    mounted(){
        if(this.score < 250) {
            this.rank = 'Ninja Fingers'
        } else if (this.score < 400) {
            this.rank = 'Rapid Reflexes'
        } else {
            this.rank = 'Snail Pace...'
        }
    }
}
</script>

<style>

</style>