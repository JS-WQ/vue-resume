<template>
  <div class="signBox">
    <div class="wrapper">
      <transition name="fade" mode="out-in">
        <div class="signup item" v-if="status === 'signup'">
          <div class="info">
            <h4>Welcome Back</h4>
            <span>To keep connected with us please login width your personal info</span>
            <p @click="change('signin')">SIGN IN</p>
          </div>
          <div class="btn">
            <i class="close iconfont icon-delete" @click="close"></i>
            <h3>Create Account</h3>
            <div class="content">
              <form @submit.prevent="signUp">
                <div class="formRow">
                  <i class="iconfont icon-yonghu"></i>
                  <input type="text" placeholder="Name" v-model="formData.username" v-focus>
                </div>
                <div class="formRow">
                  <i class="iconfont icon-youjian"></i>
                  <input type="text" placeholder="Email" v-model="formData.eMail">
                </div>
                <div class="formRow">
                  <i class="iconfont icon-mima"></i>
                  <input type="password" placeholder="Password" v-model="formData.password">
                </div>
                <div class="formActions">
                  <input type="submit" value="SIGN UP">
                  <span class="error" v-if="error !== ''">{{error}}</span>
                </div>
              </form>
            </div>
          </div>
        </div>
      </transition>
      <transition name="fade" mode="out-in">
        <div class="signin item" v-if="status === 'signin'">
          <div class="btn">
            <i class="close iconfont icon-delete" @click="close"></i>
            <h3>Sign in</h3>
            <div class="content">
              <form @submit.prevent="sigin">
                <div class="formRow">
                  <i class="iconfont icon-yonghu"></i>
                  <input type="text" placeholder="Name" v-model="formData.username" v-focus>
                </div>
                <div class="formRow">
                  <i class="iconfont icon-mima"></i>
                  <input type="password" placeholder="Password" v-model="formData.password">
                </div>
                <div class="formActions">
                  <input type="submit" value="SIGN IN">
                  <span class="error" v-if="error !== ''">{{error}}</span>
                </div>
              </form>
            </div>
          </div>
          <div class="info">
            <h4>Hello,Friend!</h4>
            <span>Enter your personal details and start journey with us</span>
            <p @click="change('signup')">SIGN UP</p>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import AV from "../learnCloud/learncloud.js";
export default {
  data() {
    return {
      formData: {
        username: "",
        password: "",
        eMail: ""
      },
      error: ""
    };
  },
  methods: {
    //登录
    sigin: function() {
      AV.User.logIn(this.formData.username, this.formData.password).then(
        () => {
          console.log("登录成功");
          
          //改变页面状态为已登录,并显示用户名
          this.$emit("success", this.formData.username);
          
          //提交获取数据请求
          this.$emit("getData");
        },
        err => {
          this.error = error;
        }
      );
    },
    //注册
    signUp: function() {
      var user = new AV.User();
      user.setUsername(this.formData.username);
      user.setPassword(this.formData.password);
      user.setEmail(this.formData.eMail);
      user.signUp().then(function(loggedInUser) {}, error => {
        this.error = error;
      });
    },
    close: function() {
      this.$emit("setSignshow", "hidden");
    },
    change: function(status) {
      this.$emit("setSignshow", status);
    }
  },
  computed: {},
  components: {},
  created() {},
  props: ["status"],
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  }
};
</script>
<style lang='less' scoped>
.signBox {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 998;
  background: #f0f4f3;
  display: flex;
  justify-content: center;
  align-items: center;
  .wrapper {
    position: relative;
    width: 740px;
    height: 468px;
    background: #fff;
    border-radius: 15px;
    box-shadow: 2px 2px 6px #aaaaaa63;
    overflow: hidden;
    .item {
      width: 740px;
      height: 468px;
      border-radius: 15px;
      display: flex;
      position: absolute;
      left: 0;
      top: 0;
      .btn {
        width: 460px;
        position: relative;
        .close {
          position: absolute;
          top: 4px;
          color: #babbbb;
          font-size: 20px;
        }
        h3 {
          color: #4fb19b;
          font-size: 28px;
          margin-top: 80px;
        }
        .content {
          width: 300px;
          margin: 0 auto;
          margin-top: 25px;
          i {
            font-size: 14px;
            padding-left: 16px;
          }
          input {
            border: none;
            outline: none;
            height: 28px;
            background: #f4f8f7;
            margin-left: 6px;
          }
          input::-webkit-input-placeholder {
            color: #babbbb;
          }
          .formRow {
            margin-bottom: 10px;
            background: #f4f8f7;
            border-radius: 5px;
            text-align: left;
            padding: 6px 0;
          }
          .formActions {
            display: inline-block;
            font-size: 13px;
            padding: 8px 60px;
            border-radius: 23px;
            background: #4fb19b;
            margin-top: 40px;
            input {
              background: #4fb19b;
              color: #fff;
              cursor: pointer;
            }
          }
        }
      }
    }
    .signup {
      .info {
        background: linear-gradient(to top right, #4eaf9d, #4ea7b2);
      }
      .close {
        right: 6px;
      }
    }
    .signin {
      .info {
        background: linear-gradient(to top right, #5dbf96, #5dafbb);
      }
      .close {
        left: 6px;
      }
    }
    .fade-enter-active,
    .fade-leave-active {
      transition: all 0.5s ease;
    }
    .fade-enter,
    .fade-leave-to {
      transform: translateX(-740px);
      opacity: 0;
    }
  }
  .info {
    width: 280px;
    padding: 120px 40px 92px 40px;
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
      cursor: pointer;
    }
  }
}
</style>