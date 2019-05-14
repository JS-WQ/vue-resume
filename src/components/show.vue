<template>
  <div class="showBox" :class="color">
    <i class="iconfont icon-shanchu" @click="recov"></i>
    <div class="message">
      <div class="username">
        <img src="../../public/icons/user.jpg">
        <li class="name">{{resume.profile.name}}</li>
        <li class="aim" v-show="resume.profile.aim">求职意向:{{resume.profile.aim}}</li>
      </div>
      <div class="usermess item">
        <h4>基本资料</h4>
        <li v-for="(value,key) in user">{{mess[key]}}: {{value}}</li>
      </div>
      <div class="contact item">
        <h4>联系方式</h4>
        <li v-for="(value,key) in resume.telephone">{{mess[key]}}: {{value}}</li>
      </div>
      <div class="skills item">
        <h4>技能特长</h4>
        <div v-for="item in resume.vocationalSkills" class="skillBox">
          <div class="wrapper" v-if="item.name">
            <span>{{item.name}}</span>
            <vslider :num="item.num" :color='color'></vslider>
          </div>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="workInfo contentInfo">
        <div class="title">
          <i class="iconfont icon-gongzuojingli"></i>
          <span>工作经历</span>
          <p></p>
        </div>
        <div class="info">
          <div class="item" v-for="item in resume.WorkExperience">
            <div class="infoTitle">
              <span>{{item.company}}</span>
              <span class="center">{{item.position}}</span>
              <span>{{item.time}}</span>
            </div>
            <div class="infoCont">
              <li class="cont">{{item.jobContent}}</li>
            </div>
          </div>
        </div>
      </div>
      <div class="projectInfo contentInfo">
        <div class="title">
          <i class="iconfont icon-xiangmu"></i>
          <span>项目经历</span>
          <p></p>
        </div>
        <div class="info">
          <div class="item" v-for="item in resume.Projects">
            <div class="infoTitle">
              <span>{{item.name}}</span>
            </div>
            <div class="infoCont">
              <li class="cont">{{item.contents}}</li>
              <li>
                <span class="link" v-show="item.objlink">项目地址:</span>
                {{item.objlink}}
              </li>
            </div>
          </div>
        </div>
      </div>
      <div class="studyInfo contentInfo">
        <div class="title">
          <i class="iconfont icon-xuexi"></i>
          <span>学习经历</span>
          <p></p>
        </div>
        <div class="info">
          <div class="item" v-for="item in resume.StudyExperience">
            <div class="infoTitle">
              <span>{{item.school}}</span>
              <span class="center">{{item.time}}</span>
              <span>{{item.degree}}</span>
            </div>
          </div>
        </div>
      </div>
      <div class="awardsInfo contentInfo">
        <div class="title">
          <i class="iconfont icon-guanjunhuojiang"></i>
          <span>获得荣誉</span>
          <p></p>
        </div>
        <div class="info">
          <li v-for="item in resume.Awards" class="itemli" v-show="item.contents">{{item.contents}}</li>
        </div>
      </div>
      <div class="contentInfo selfAppraisal">
        <div class="title">
          <i class="iconfont icon-evaluate"></i>
          <span>自我评价</span>
          <p></p>
        </div>
        <div class="info">
          <li class="selfcont">{{resume.selfAppraisal.content}}</li>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import slider from './slider'
export default {
  data () {
    return {
      mess: {
        city: '城市',
        birth: '出生年月',
        aim: '求职意向',
        workTime: '工作年限',
        money: '薪资要求',
        degree: '学历',
        phone: '手机',
        QQ: 'QQ',
        wechat: '微信',
        mail: '邮箱',
        adress: '地址'
      }
    }
  },
  methods: {
    recov: function () {
      this.$emit('toRecovery')
    }
  },
  computed: {
    user: function () {
      let empty = JSON.parse(JSON.stringify(this.resume.profile))
      for (let key in empty) {
        if (key === 'name' || key === 'aim') {
          delete empty[key]
        }
      }
      return empty
    }
  },
  components: {
    vslider: slider
  },
  created () {},
  props: ['resume', 'color']
}
</script>
<style lang='less' scoped>
.showBox {
  max-width: 1000px;
  display: flex;
  font-family: "微软雅黑";
  padding: 20px;
  align-items: flex-start;
  overflow: auto;
  min-height: 100%;
  position: relative;
  .icon-shanchu {
    position: absolute;
    right: 0px;
    font-size: 30px;
    display: none;
  }
  .message {
    width: 300px;
    padding-left: 20px;
    min-height: 950px;
    .username {
      margin-top: 25px;
      margin-bottom: 30px;
      .name {
        font-size: 26px;
        font-weight: 700;
        letter-spacing: 2px;
      }
      .aim {
        font-size: 20px;
        letter-spacing: 4px;
      }
      img {
        border: 3px solid #ffffff;
        border-radius: 3px;
      }
    }
    .item {
      text-align: left;
      margin-bottom: 30px;
    }
    .skillBox {
      padding-right: 15px;
      margin-bottom: 15px;
      .wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
    }
    h4 {
      font-size: 22px;
      font-weight: 600;
      margin-bottom: 18px;
    }
    li {
      font-size: 18px;
      margin-bottom: 4px;
    }
  }
  .content {
    min-height: 950px;
    text-align: left;
    padding-left: 20px;
    min-width: 700px;
    .title {
      .iconfont {
        font-size: 26px;
      }
      span {
        font-size: 26px;
        margin-left: 22px;
        margin-right: 50px;
        font-weight: 500;
      }
      p {
        display: inline-block;
        width: 180px;
        height: 3px;
      }
    }
    .contentInfo {
      margin-bottom: 20px;
      .title {
        margin-bottom: 10px;
      }
      .info {
        .itemli {
          list-style-type: square;
        }
        .item {
          margin-bottom: 10px;
          .infoTitle {
            margin-bottom: 3px;
            span {
              font-weight: 700;
              display: inline-block;
            }
            .center {
              margin: 0 30px;
            }
          }
          .infoCont {
            .cont {
              line-height: 28px;
            }
            .link {
              font-weight: 600;
            }
          }
        }
        .selfcont {
          line-height: 28px;
          text-indent: 28px;
        }
      }
    }
  }
}
.normal {
  .message {
    background-color: #35343a;
    color: #ffffff;
    .username {
      color: #ffa527;
    }
    h4 {
      color: #ffa527;
    }
  }
  .content {
    .title {
      .iconfont {
        color: #f8751f;
      }
      span {
        color: #f8751f;
      }
      p {
        background: radial-gradient(#f8751f -24%, white 100%);
      }
    }
  }
}
.green {
  .message {
    background-color: #5dd5c8;
    color: #ffffff;
    .username {
      color: #00c2b3;
    }
  }
  .content {
    .title {
      .iconfont {
        color: #00c2b3;
      }
      span {
        color: #00c2b3;
      }
      p {
        background: radial-gradient(#5dd5c8 -24%, white 100%);
      }
    }
  }
}
.black{
  .message {
    background-color: #000;
    color: #9d9d9d;
    .username {
      color: #ffffff;
    }
    h4 {
      color: #a0a0a0;
    }
  }
  .content {
    .title {
      .iconfont {
        color: #525252;
      }
      span {
        color: #525252;
      }
      p {
        background: radial-gradient(#525252 -24%, white 100%);
      }
    }
  }
}
.showBox::-webkit-scrollbar {
  display: none;
}
</style>
