<template>
  <div class="slide-show" @mouseover="stopSlider" @mouseout="startSlider">
    <div class="slide-show-container">
      <div class="img-container">
        <transition name="slider-trans">
          <img v-if="isShow" :src="sliders[nowIndex].src" alt="">
        </transition>
        <transition name="slider-trans-old">
          <img v-if="!isShow" :src="sliders[nowIndex].src" alt="">
        </transition>
      </div>
      <div class="slid-pages">
          <span class="slid-pages-title">{{sliders[nowIndex].title}}</span>
          <ul class="slid-pagenation">
            <li @click="goSlider (prevIndex)">&lt;</li>
            <!-- <li class="active" v-for="(item,index) in slides">{{index+1}}</li> -->
            <li 
            :class="{active: index === nowIndex}" 
            v-for="(item ,index) in sliders" 
            v-bind:key="item.title"
            @click="goSlider (index)"
            >{{index+1}}</li>
            <li @click="goSlider (nextIndex)">&gt;</li>
          </ul>
      </div>
      <div class="slid-prev"></div>
      <div class="slid-next"></div>
    </div>
  </div>
</template>
<script>
export default {
  props:{
    sliders: {
      type: Array,
      default: function () {
        return [
          {
            src: require('../assets/slideShow/pic1.jpg'),
            title: '加载中',
            href: 'detail/analysis'
          },
        ]
      }
    },
    initTime:{
      type:Number,
      default:1000
    }
  },
  data () {
    return {
      nowIndex: 0,
      isShow: true
    }
  },
  methods : {
    goSlider (goIndex) {
      this.isShow = false;
      setTimeout(() => {
        this.isShow = true;
        this.nowIndex = goIndex;
      }, 10);
    },
    autoPlay () {
      this.invId=setInterval(() => {
        this.goSlider(this.nextIndex)
      },this.initTime)
    },
    clearInv () {
      clearInterval(this.invId)
    },
    stopSlider () {
      this.clearInv();
    },
    startSlider () {
      this.autoPlay();
    }
  },
  computed:{
    prevIndex () {
      if( this.nowIndex === 0){
        return this.sliders.length-1;
      }else{
        return this.nowIndex-1;
      } 
    },
    nextIndex () {
      if( this.nowIndex === this.sliders.length-1){
        return 0;
      }else{
        return this.nowIndex+1;
      }
    }
  },
  mounted () {
    this.autoPlay();
  }
}
</script>
<style scoped>
  .slide-show{
    margin-bottom: 10px;
    position: relative;
    overflow: hidden;
    margin-top: 15px;
  }
  /* .slide-trans-enter-active {
  transition: all .5s;
  }
  .slide-trans-enter {
    transform: translateX(-900px);
    opacity: 0;
  }
  .slide-trans-old-leave-active {
    transition: all .5s;
    transform: translateX(900px);
    opacity: 0;
  } */
  .img-container{
    width: 900px;
    height: 300px;
    overflow: hidden;
    margin-top: 15px;
    
  }
  .img-container:after{
    content: '';
    display: block;
    overflow: hidden;
  }
 
  .img-container img{
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
  .slid-pages{
    width:100%;
    height: 30px;
    line-height: 30px;
    color: #fff;
    position: absolute;
    left: 0;
    bottom: 0;
    background-color: black;
    opacity: 0.7;
  }
  .slid-pages:after{
    content: '';
    display: block;
    clear: both;
  }
  .slid-pages-title{
    float: left;
    margin-left: 10px;
  }
  .slid-pagenation{
    float: right;
    margin-right: 20px;
  }
  .slid-pagenation li{
    float: left;
    margin:0 5px;
    cursor: pointer;
  }
  .slid-pagenation .active{
    text-decoration: underline;
  }
</style>