<template>
  <div  class="count-component">
    <button :class="nowCount === min?'default-button':'act-button'" @mousedown="subEvent">-</button>
    <input type="text" @keyup="inputChange" v-model="nowCount">
    <button :class="nowCount === max?'default-button':'act-button'" @mousedown="mulEvent">+</button>
  </div>
  
</template>

<script>
export default {
    props:{
        max: {
            type: Number,
            default: 5
        },
        min: {
            type: Number,
            default: 1
        }
    },
    data () {
        return{
            nowCount:this.min
        }
    },
    watch:{
        nowCount (){
            this.$emit(changeNum,this.nowCount)
        }
    },
    methods:{
        subEvent () {
            if(this.nowCount > this.min){
                this.nowCount--
            }else{
                this.nowCount = this.min
            }
        },
        mulEvent () {
            if(this.nowCount < this.max){
                this.nowCount++
            }else{
                this.max
            }
        },
        inputChange () {
            let fix
            if(typeof this.nowCount === "string"){
                fix = Number(this.nowCount.replace(/\D/g,''))
            }else{
                fix=this.nowCount
            }
            if(fix > this.max || fix < this.min){
                fix = this.min
            }
            this.nowCount=fix
        }
    }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.count-component{
    vertical-align: middle;
}
.count-component .default-button{
    height: 24px;
    border:1px solid #ccc;
    background: #fff;
    color: #333;
    padding:0 10px;
    line-height: 24px;
    outline: none;
}
.count-component input{
    height: 22px;
    line-height: 24px;
    text-align: center;
    width:50px;
    border:1px solid #ccc;
    margin: 0;
    padding: 0;
    outline: none;
}
.count-component .act-button{
    height: 24px;
    border:1px solid #ccc;
    background: #4fc08d;
    color: #fff;
    padding:0 10px;
    line-height: 24px;
    outline: none;
}
</style>
