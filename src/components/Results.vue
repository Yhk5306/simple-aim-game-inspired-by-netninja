<template>
  <p>You ve hit  {{count}} head shoots</p>
  <p class="rank">{{rank}}</p>
</template>

<script>
export default {
  props:['score','count'],
  data(){
    return{
      rank:null
    }
  },
  mounted() {
    console.log(this.count)
    if (this.count > 18){
      this.rank = 'Good job vise one'
    }else if (this.count > 15){
      this.rank = 'Pff What is this'
    }else {
      this.rank = 'You suck leave it'
    }
  }
}
</script>
<style>
.rank{
  font-size: 1.4em;
  color: #0faf87;
  font-weight: bold;
}
</style>