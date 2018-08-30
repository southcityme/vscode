<template>

  <div v-if="isShow" class="dialog">
    <transition name="fall-down">
      <div class="diaLogBox" v-if="isShow">
        <p @click="closeDiaLog" class="closeDiaLog">X</p>
        <slot></slot>
      </div>
    </transition>
  </div>
  
</template>

<script>
export default {
  props: {
    isShow: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      msg: 'loading......'
    }
  },
  methods:{
    closeDiaLog (){
      this.$emit('on-close')
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.dialog{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.8);
    text-align: center;
}
.diaLogBox{
    min-width: 20%;
    display: inline-block;
    border:1px solid #fff;
    padding: 10px;
    background-color: #fff;
    margin-top: 20%;
    text-align: left;
    position: relative;
}
.closeDiaLog{
  position: absolute;
  width:30px;
  height: 30px;
  line-height: 30px;
  text-align: center;
  font-size: 18px;
  right: 0;
  top: 0;
  cursor: pointer;
}
.fall-down-enter{
  transform: translateY(-300px);
  opacity: 0;
}
.fall-down-enter-active,.fall-down-leave-active{
  transition: transform .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.fall-down-leave-to{
  transform: translateY(300px);
  opacity: 0;
}
</style>
