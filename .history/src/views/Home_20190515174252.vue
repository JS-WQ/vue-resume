<template>
  <div class="home" ref="home">
    <vheader @toPreview="toPreview" @setSignshow='setSignshow'></vheader>
    <div class="contentBox">
      <vnavBtn :resume="resume" @setColor="setColor"></vnavBtn>
      <vshow :resume="resume" @toRecovery="toRecovery" ref="showbox" :color="color"></vshow>
    </div>
    <vsignbox @getData="getData" v-if="signShow"></vsignbox>
  </div>
</template>

<script>
import header from "../components/header";
import navBtn from "../components/nav";
import show from "../components/show";
import signbox from "../components/signBox";
import AV from "../learnCloud/learncloud.js";

export default {
  data() {
    return {
      resume: {
        profile: {
          name: "",
          city: "",
          birth: "",
          workTime: "",
          aim: "",
          degree: "",
          money: ""
        },
        WorkExperience: [
          { company: "", jobContent: "", position: "", time: "" }
        ],
        StudyExperience: [{ school: "", time: "", degree: "" }],
        Projects: [{ name: "", contents: "", objlink: "" }],
        Awards: [{ contents: "" }],
        vocationalSkills: [{ name: "", num: 0 }],
        telephone: { phone: "", QQ: "", wechat: "", mail: "", adress: "" },
        selfAppraisal: { content: "" }
      },
      color: "normal",
      signShow:false
    };
  },
  components: {
    vheader: header,
    vnavBtn: navBtn,
    vshow: show,
    vsignbox: signbox
  },
  methods: {
    toPreview: function() {
      this.$refs.home.classList.add("preview");
    },
    toRecovery: function() {
      this.$refs.home.classList.remove("preview");
    },
    setColor: function(val) {
      this.color = val;
    },
    //从网站获取数据
    getData: function() {
      var query = new AV.Query("IRusmer");
      query.descending("createdAt");
      query.include("IRusmer");
      query.include("IRusmer.targetAVUser");
      query.find().then(mess => {
        mess.forEach(product => {
          var imx = product.get("imx");
          this.iresum.imx = product.get("imx");
          this.iresum.workExpress = product.get("workExpress");
          this.iresum.studyExpress = product.get("studyExpress");
          this.iresum.itemsdemo = product.get("itemsdemo");
          this.iresum.prizes = product.get("prizes");
        });
      });
    },
    //设置登录框是否显示
    setSignshow:function(flage){
      this.signShow = flage
    }
  },
  mounted() {}
};
</script>
<style lang="less">
.home {
  display: flex;
  flex-direction: column;
  height: 100%;
  position: relative;
  .contentBox {
    flex: 1;
    display: flex;
  }
}
.preview {
  .header {
    display: none;
  }
  .contentBox {
    .editor {
      display: none;
    }
    .showBox {
      margin-left: 50px;
      .iconfont.icon-shanchu {
        display: block;
      }
    }
  }
}
</style>
