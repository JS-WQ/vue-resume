<template>
  <div class="signBox">
    <div class="wrapper">
      <div class="signup item">
        <div class="left info">
          <h4>Welcome Back</h4>
          <span>To keep connected with us please login width your personal info</span>
          <p>SIGN IN</p>
        </div>
        <div class="btn"></div>
      </div>
      <div class="signin item">
        <div class="btn"></div>
        <div class="right info"></div>
      </div>
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
    overflow: hidden;
    .item {
      width: 740px;
      height: 468px;
      border-radius: 15px;
      display: flex;
      .btn{
        width: 460px;
      }
    }
    .signup {
      display: none;
    }
    .signin{
    }
  }
  .info {
    width: 280px;
    padding: 120px 40px 92px 40px;
    background: linear-gradient(to top right, #5dbf96, #4eafa1);
    color: #fff;
    h4 {
      font-size: 28px;
    }
    span {
      display: inline-block;
      font-size: 13px;
      line-height: 22px;
      margin-top: 28px;
      margin-bottom: 34px;
      color: #ffffffbf;
    }
    p {
      display: inline-block;
      font-size: 13px;
      color: #ffffffde;
      border: 1px solid #fff;
      padding: 13px 60px;
      border-radius: 23px;
    }
  }
}
</style>