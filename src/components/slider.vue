<template>
  <div class="slider" :class="color">
    <div class="content" ref="content"></div>
    <div class="num">{{num}}%</div>
  </div>
</template>

<script>
export default {
  data () {
    return {}
  },
  methods: {
    setWidth: function (num) {
      let iwidth = (num / 100) * 180
      this.$refs.content.style.width = iwidth + 'px'
    }
  },
  watch: {
    num: function () {
      this.setWidth(this.num)
    }
  },
  computed: {},
  components: {},
  created () {
  },
  mounted () {
    this.setWidth(this.num)
  },
  props: ['num', 'color']
}
</script>
<style lang='less' scoped>
.slider {
  display: flex;
  height: 8px;
  width: 180px;
  background: #e6e6e6;
  justify-content: left;
  align-items: center;
  border-radius: 8px;
  .content {
    height: 8px;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
  }
  .num {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    font-size: 12px;
    line-height: 24px;
  }
}
.normal{
  .content{
    background: #ffa527;
  }
  .num{
    background: #ffa527;
  }
}
.green{
  .content{
    background: #00bcd4e8;
  }
  .num{
    background: #00bcd4e8;
  }
}
.black{
  .content{
    background: #9E9E9E;
  }
  .num{
    background: #9E9E9E;
    color: #ffffff;
  }
}
</style>
