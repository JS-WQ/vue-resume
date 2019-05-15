<template>
  <div class="header">
    <span class="title">Resume</span>
    <div class="headRight">
      <el-button @click="toSignUp">注册</el-button>
      <el-button type="primary" @click="toSignIn">登录</el-button>
      <div class="userbox" v-if="state">
        <span>你好</span>
        <el-button type="info" @click="keepDate">预览</el-button>
        <el-button type="info" @click="show">预览</el-button>
        <el-button type="warning" @click="leave">退出</el-button>
      </div>
    </div>
  </div>
</template>

<script>
import AV from "../learnCloud/learncloud.js";

export default {
  data() {
    return {};
  },
  methods: {
    show: function() {
      this.$emit("toPreview");
    },
    toSignUp: function() {
      this.$emit("setSignshow", "signup");
    },
    toSignIn: function() {
      this.$emit("setSignshow", "signin");
    },
    //退出登录
    leave: function() {
      AV.User.logOut();
    },
    //保存数据
    keepDate: function() {
      var IRusmer = AV.Object.extend("IRusmer");
      var irusmer = new IRusmer();

      //权限设置 登录账号拥有读写权力
      var acl = new AV.ACL();
      acl.setPublicReadAccess(false);
      acl.setPublicWriteAccess(false);
      acl.setReadAccess(AV.User.current(), true);
      acl.setWriteAccess(AV.User.current(), true);
      irusmer.setACL(acl);
      irusmer.set("profile", this.resume.profile);
      irusmer.set("WorkExperience", this.resume.WorkExperience);
      irusmer.set("StudyExperience", this.resume.StudyExperience);
      irusmer.set("Projects", this.resume.Projects);
      irusmer.set("Awards", this.resume.Awards);
      irusmer.set("telephone", this.resume.telephone);
      irusmer.set("selfAppraisal", this.resume.selfAppraisal);
      irusmer.set("vocationalSkills", this.resume.vocationalSkills);
      irusmer.save();
    }
  },
  computed: {},
  components: {},
  created() {},
  props: ["state"]
};
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
