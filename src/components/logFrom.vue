<template>
  <div class="log-from">
      <div class="detail-lable">
          <span>用户名</span>
          <input v-model="userName" type="text">
          <span>{{userErros.errorText}}</span>
      </div>
      <div class="detail-lable">
          <span>密码</span>
          <input v-model="password" type="password">
          <span>{{passErros.errorText}}</span>
      </div>
      <div class="detail-lable">
        <button class="logButton" @click="toLog">确认</button>
         <span>{{lastCheck}}</span>
      </div>
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
  computed:{
    userErros () {
      let errorText, status
      if (!/@/g.test(this.userName)) {
        status = false
        errorText = '不包含@'
      }else{
        status = true
        errorText = ''
      }
      if(!this.userFlag){
        this.userFlag = true
        errorText = ''
      }
      return {
        status,
        errorText
      }
    },
    passErros () {
      let errorText, status
      if (!/^\w{1,6}$/g.test(this.password)) {
        status = false
        errorText = '位数不正确'
      }else{
        status = true
        errorText = ''
      }
      if(!this.passFlag){
        this.passFlag = true
        errorText = ''
      }
      return {
        status,
        errorText
      }
    },
  },
  data () {
    return {
      userName:'',
      password:'',
      errorText: '',
      lastCheck:''
    }
  },
  methods:{
    closeDiaLog () {
      this.$emit('on-close')
    },
    toLog () {
      if( this.userErros.status && this.passErros.status){
        this.lastCheck=''
        this.$http.post('api/login')
        .then((res) => {
          this.$emit('has-log', res.data)
        }, (error) => {
          console.log(error)
        })
      }else{
         this.lastCheck = '请正确输入相关用户信息'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.detail-lable{
  padding: 0 20px;
  width:400px;
  margin:20px 0;
}
.detail-lable span:first-child{
  display: inline-block;
  width:50px;
}
.detail-lable span:last-child{
  color: red;
}
.detail-lable input{
  outline: none;
  padding-left: 10px;
  border:1px solid #ccc;
}
.detail-lable input:focus{
  border:1px solid #000;
}
.logButton{
  width:80px;
  border:none;
  color: #fff;
  background: #4fc08d;
  height: 30px;
}
</style>
