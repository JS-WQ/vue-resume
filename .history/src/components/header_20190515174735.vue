<template>
  <div class="header">
    <span class="title">Resume</span>
    <div class="headRight">
      <el-button @click="toSignUp">注册</el-button>
      <el-button type="primary" @click="toSignIn">登录</el-button>
      <el-button type="info" @click="show">预览</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {}
  },
  methods: {
    show: function () {
      this.$emit('toPreview')
    }, 
    toSignUp:function(){
      this.$emit('setSignshow','signup')
    },
    toSignIn:function(){
      this.$emit('setSignshow','signip')
    }
    
  },
  computed: {},
  components: {},
  created () {}
}
</script>
<style lang='less' scoped>
.header {
  text-align: left;
  padding: 14px 40px;
  border-bottom: 1px solid #e6e6e6;
  display: flex;
  justify-content: space-between;
  .title {
    font-size: 38px;
    font-weight: 700;
    margin-left: 20px;
  }
}
</style>
