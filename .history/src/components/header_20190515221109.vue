<template>
  <div class="header">
    <span class="title">Resume</span>
    <div class="headRight">
      <div v-if="!state">
        <el-button @click="toSignUp">注册</el-button>
        <el-button type="primary" @click="toSignIn">登录</el-button>
      </div>
      <div class="userbox" v-if="state">
        <span>你好,{{username}}</span>
        <el-button type="success" @click="keepDate">保存</el-button>
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
      location.reload()
    },
    //保存数据
    keepDate: function() {
      //id存在，更新数据，否则新建数据
      if(this.id !== ''){
        this.updata()
      }else{
        this.creatdata()
      }
    },
    //更新数据
    updata: function() {
      let irusmer = AV.Object.createWithoutData('IRusmer', this.id)
      irusmer.set("profile", this.resume.profile);
      irusmer.set("WorkExperience", this.resume.WorkExperience);
      irusmer.set("StudyExperience", this.resume.StudyExperience);
      irusmer.set("Projects", this.resume.Projects);
      irusmer.set("Awards", this.resume.Awards);
      irusmer.set("telephone", this.resume.telephone);
      irusmer.set("selfAppraisal", this.resume.selfAppraisal);
      irusmer.set("vocationalSkills", this.resume.vocationalSkills);
      irusmer.save().then(
        ()=> {
          this.$emit('showNotice')
        },
        function(error) {
          console.error(error);
        }
      )
    },
    //新建数据
    creatdata: function() {
      let IRusmer = AV.Object.extend("IRusmer");
      let irusmer = new IRusmer();
      //权限设置 登录账号拥有读写权力
      let acl = new AV.ACL();
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
      irusmer.save().then(
        ()=> {
          this.$emit('showNotice')
        },
        function(error) {
          console.error(error);
        }
      )
    }
  },
  computed: {},
  components: {},
  created() {},
  props: ["state", "resume", "username",'id']
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
  .userbox{
    span{margin-right: 10px}
  }
}
</style>
