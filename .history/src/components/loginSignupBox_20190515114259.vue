<template>
  <div class="loginSignup">
      <div class="login">
        <div class="left">

        </div>
        <div class="right"></div>
      </div>
      <div class="signin"></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
    };
  },
  methods: {},
  computed: {},
  components: {},
  created() {}
}

</script>
<style lang='less' scoped>
.loginSignup{
  position: absolute;
  transform:translate3d(-50%,-50%,0);
  z-index: 999;
  .login{
    width: 740px;
    height: 468px;
    border: 1px solid red;
    border-radius: 8px;
    .left{
      width: 280px;
    }
    .right{
      width: 460px;
    }
  }

}
</style>