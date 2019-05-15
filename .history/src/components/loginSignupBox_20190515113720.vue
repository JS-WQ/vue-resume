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
  .login{
    width: 745px;
    height: 468px;
    border: 1px solid red;
    border-radius: 8px;
    .left{
      width: 240px;
    }
    .right{
      width: 400px;
    }
  }

}
</style>