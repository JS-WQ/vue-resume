<template>
  <div class="home" ref="home">
    <vheader @toPreview="toPreview"></vheader>
    <div class="contentBox">
      <vnavBtn :resume="resume" @setColor="setColor" @getData='getData'></vnavBtn>
      <vshow :resume="resume" @toRecovery="toRecovery" ref="showbox" :color="color"></vshow>
    </div>
    <vsignbox></vsignbox>
  </div>
</template>

<script>
import header from "../components/header";
import navBtn from "../components/nav";
import show from "../components/show";
import signbox from "../components/signBox";
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
      color: "normal"
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
