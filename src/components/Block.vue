<template>
  <div class="block" v-if="showBlock" @click="stopTimer" :style="{left:Math.floor(Math.random()*(90-0+1)+0)+'%',top:Math.floor(Math.random()*(90-0+1)+0)+'%'}">
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" class="iconify iconify--ant-design" width="32" height="32" preserveAspectRatio="xMidYMid meet" viewBox="0 0 1024 1024"><path fill="currentColor" d="M952 474H829.8C812.5 327.6 696.4 211.5 550 194.2V72c0-4.4-3.6-8-8-8h-60c-4.4 0-8 3.6-8 8v122.2C327.6 211.5 211.5 327.6 194.2 474H72c-4.4 0-8 3.6-8 8v60c0 4.4 3.6 8 8 8h122.2C211.5 696.4 327.6 812.5 474 829.8V952c0 4.4 3.6 8 8 8h60c4.4 0 8-3.6 8-8V829.8C696.4 812.5 812.5 696.4 829.8 550H952c4.4 0 8-3.6 8-8v-60c0-4.4-3.6-8-8-8zM512 756c-134.8 0-244-109.2-244-244s109.2-244 244-244s244 109.2 244 244s-109.2 244-244 244z"></path><path fill="currentColor" d="M512 392c-32.1 0-62.1 12.4-84.8 35.2c-22.7 22.7-35.2 52.7-35.2 84.8s12.5 62.1 35.2 84.8C449.9 619.4 480 632 512 632s62.1-12.5 84.8-35.2C619.4 574.1 632 544 632 512s-12.5-62.1-35.2-84.8C574.1 404.4 544.1 392 512 392z"></path></svg>
  </div>
</template>

<script>
var audio = new Audio('/asset.mp3')
var sound = new Audio('/voice.mp3')
export default {
  props:['delay','difficulty'],
  data(){
    return {
      showBlock:false,
      timer:null,
      reactionTime:0,
      showTime:null,
      holdTime:0,
    }
  },
  mounted() {
    setTimeout(()=> {
      this.showBlock = true
      this.startTimer()
      this.counter()
      this.closeCounter()
    },this.delay)
  },
  methods:{
    startTimer(){
      this.timer = setInterval(() => {
        this.reactionTime += 10
      },10)
    },
    counter(){
      const delay = 1.4;
      const limit = 10;
      let i = 1;

      console.log('START!');
      const limitedInterval = setInterval(() => {
        audio.play();
        this.showBlock = true

        console.log(`message ${i}, appeared after ${delay * i++} seconds`);

        if (i > limit) {
          clearInterval(limitedInterval);
          console.log('interval cleared!');
        }
      }, delay * 1000);
    },
    closeCounter(){
      const delay = 1.5;
      const limit = 10;
      let i = 1;

      console.log('START!');
      const limitedInterval = setInterval(() => {
        this.showBlock = false

        console.log(`message ${i}, appeared after ${delay * i++} seconds`);

        if (i > limit) {
          clearInterval(limitedInterval);
          this.$emit('end',this.reactionTime)
          console.log('interval cleared!');
        }
      }, delay * 1000);
    },
    stopTimer(){
      sound.play()
      clearInterval(this.timer)
    }
  }
}
</script>
<style>
svg {
  pointer-events: none;
}
body{
  position:relative;
}
.block{
  position: absolute;
  display: flex;
  text-align: center;
  align-items: center;
  width:100px;
  height: 100px;
  border-radius: 20px;
  background: #0faf87;
  color: #f2f2f2;
  border: 10px solid transparent;
  cursor: pointer;
  justify-content: center;
}
</style>