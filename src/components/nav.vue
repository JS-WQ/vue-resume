<template>
  <div class="editor">
    <div class="nav">
      <li v-for="(item,index) in data" :class="{'active':index === status}" @click="chance(index)">
        <p :class="item.class"></p>
        <span>{{item.text}}</span>
      </li>
      <div class="setColor">
        <div class="btn">
          <p class="iconfont icon-peise"></p>
          <span>选择简历配色</span>
        </div>
        <div class="colorCt">
          <li class="normal" @click="setCo('normal')"></li>
          <li class="green" @click="setCo('green')"></li>
          <li class="black" @click="setCo('black')"></li>
        </div>
      </div>
    </div>
    <transition name="fade" mode="out-in">
      <veditor
        :navIndex="status"
        :demo="resume[demoName[status]]"
        :key="status"
        :detailShow="detailShow"
        v-if="detailShow"
        @closeDetail="closeDetail"
      ></veditor>
    </transition>
  </div>
</template>

<script>
import editorDetail from './editor-detail'
export default {
  data () {
    return {
      status: 0,
      data: [
        { text: '身份信息', class: 'iconfont icon-shenfenzheng' },
        { text: '工作经历', class: 'iconfont icon-gongzuojingli' },
        { text: '学习经历', class: 'iconfont icon-xuexi' },
        { text: '项目信息', class: 'iconfont icon-xiangmu' },
        { text: '获得荣誉', class: 'iconfont icon-guanjunhuojiang' },
        { text: '联系方式', class: 'iconfont icon-lianxi' },
        {
          text: '职业技能',
          class: 'iconfont icon-gerenzhongxin-zhuanyejineng'
        },
        { text: '自我评价', class: 'iconfont icon-evaluate' }
      ],
      detailShow: true,
      demoName: [
        'profile',
        'WorkExperience',
        'StudyExperience',
        'Projects',
        'Awards',
        'telephone',
        'vocationalSkills',
        'selfAppraisal'
      ],
      color: 'normal'
    }
  },
  methods: {
    chance: function (index) {
      this.status = index
      this.detailShow = true
    },
    closeDetail: function () {
      this.detailShow = false
    },
    setCo: function (val) {
      this.$emit('setColor', val)
    }
  },
  computed: {},
  components: {
    veditor: editorDetail
  },
  created () {},
  props: ['resume']
}
</script>
<style lang='less' scoped>
.editor {
  display: flex;
  .nav {
    width: 200px;
    padding-top: 20px;
    padding-right: 20px;
    border-right: 1px solid #e6e6e6;
    position: relative;
    z-index: 4;
    background: #fff;
    li {
      margin-bottom: 20px;
      margin-left: 20px;
      text-align: left;
      border-radius: 12px;
      cursor: pointer;
      p {
        display: inline-block;
        width: 32px;
        height: 32px;
        background: #e9e3fd6e;
        line-height: 32px;
        border-radius: 7px;
        text-align: center;
        margin-left: 6px;
      }
      p::before {
        color: #8a8a8a;
      }
      span {
        font-size: 16px;
        padding-left: 10px;
        color: #bbbec9;
      }
      .iconfont:before {
        font-size: 20px;
      }
    }
    .active {
      background: #e9e3fd;
      p::before {
        color: #ad90fc;
      }
      span {
        color: #000;
      }
    }
    .setColor {
      .btn {
        margin-bottom: 12px;
        p {
          display: inline-block;
          width: 32px;
          height: 32px;
          background: #e9e3fd6e;
          line-height: 32px;
          border-radius: 7px;
          text-align: center;
          margin-left: 6px;
        }
        p::before {
          color: #8a8a8a;
        }
        span {
          font-size: 16px;
          padding-left: 10px;
          color: #bbbec9;
        }
        .iconfont:before {
          font-size: 20px;
        }
      }
      .colorCt{
        li{
          display: inline-block;
          width: 20px;
          height: 20px;
        }
        .normal{
          background: #ffa527;
        }
        .green{
          background: #5dd5c8;
        }
        .black{
          background: #000;
        }
      }
    }
  }
  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.5s linear;
  }
  .fade-enter,
  .fade-leave-to {
    transform: translateX(-300px);
    opacity: 0;
  }
  .content {
    width: 300px;
    border-right: 1px solid #e6e6e6;
  }
}
</style>
