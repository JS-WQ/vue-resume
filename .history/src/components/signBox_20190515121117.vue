<template>
  <div class="signBox">
    <div class="wrapper">
      <div class="signup">
        <div class="left">
          <h4>Welcome Back</h4>
          <span>To keep connected with us please login width your personal info</span>
          <p>SIGN IN</p>
        </div>
        <div class="right"></div>
      </div>
      <div class="signin"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {},
  computed: {},
  components: {},
  created() {}
};
</script>
<style lang='less' scoped>
.signBox {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 998;
  background: #f0f4f3;
  .wrapper {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate3d(-50%, -50%, 0);
    background: #fff;
    border-radius: 15px;
    box-shadow: 2px 2px 6px #aaaaaa63;
    .signup {
      width: 740px;
      height: 468px;
      border-radius: 15px;
      .left {
        width: 280px;
        padding: 120px 40px 92px 40px;
      }
      .right {
        width: 460px;
      }
    }
  }
}
</style>