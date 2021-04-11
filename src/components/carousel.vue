<template>
<div>
  <transition-group tag="div" class="container" :name= transitionName>
    <div class="page" v-for="(img,index) of images" :key="index" v-show="index===show">
      <img :src="img.src" />
    </div>
  </transition-group>
  <button @click="SetShow(show-1)">-</button>
  <span>
    <button v-for="num of images.length" :key="num-1" @click="SetShow(num-1)">{{num}}</button>
  </span>
  <button @click="SetShow(show+1)">+</button>
  </div>
</template>
<script>
// let timer
const interval = 2000
export default {
  data () {
    return {
      transitionName: 'left-in',
      show: 0,
      images: [
        { src: 'https://picsum.photos/480/320?random=1' },
        { src: 'https://picsum.photos/480/320?random=2' },
        { src: 'https://picsum.photos/480/320?random=3' },
        { src: 'https://picsum.photos/480/320?random=4' },
        { src: 'https://picsum.photos/480/320?random=5' }
      ]
    }
  },
  mounted () {
    setInterval(this.nextShow, interval)
  },
  methods: {
    SetShow (index) {
      this.show = index
      // if (index < 0) {
      //   this.transitionName = 'left-in'
      //   this.show = this.images.length - 1
      // } else if (index > this.images.length - 1) {
      //   this.transitionName = 'right-in'
      //   this.show = 0
      // } else {
      //   this.transitionName = this.show < index ? 'right-in' : 'left-in'
      //   this.show = index
      // }
    },
    nextShow () {
      this.show++
    }

  },
  watch: {

    show (nVal, oVal) {
      // 防止直接修改show資料
      if (nVal < 0) {
        this.show = this.images.length - 1
      } else if (nVal > this.images.length - 1) {
        this.show = 0
      } else {
        if (oVal < 0) this.transitionName = 'left-in'
        else if (oVal > this.images.length - 1) this.transitionName = 'right-in'
        else this.transitionName = nVal > oVal ? 'right-in' : 'left-in'
      }
    }
  }

}
</script>
<style scoped>
.right-in-enter-from{
  left: 100%;
}
.right-in-enter-active{
  transition: left 0.5s;
}
.right-in-enter-to{
  left: 0%;
}
.right-in-leave-from{
  right: 0%;
}
.right-in-leave-active{
  transition: right 0.5s;
}
.right-in-leave-to{
  right: 100%;
}
.left-in-enter-from{
  right: 100%;
}
.left-in-enter-active{
  transition: right 0.5s;
}
.left-in-enter-to{
  right: 0%;
}
.left-in-leave-from{
  left: 0%;
}
.left-in-leave-active{
  transition: left 0.5s;
}
.left-in-leave-to{
  left: 100%;
}
.container {
  position: relative;
  width: 480px;
  height: 320px;
  margin: 0 auto;
  overflow: hidden;
}
.page {
  position: absolute;
  width: 480px;
  height: 320px;
}
</style>
