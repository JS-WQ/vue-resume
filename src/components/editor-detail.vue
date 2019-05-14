<template>
  <div class="detail" ref="detail">
    <i class="el-icon-close" @click="close"></i>
    <div class="editor" v-for="(item,index) in data" v-if='index === navIndex'>
        <li class="title">{{item.title}}</li>
        <div class="content">
            <div v-for="(mess,index) in demo" class="wrapper" v-if="demo.length >0 && navIndex !== 6">
                <i class="el-icon-close" @click="deletItem(index)"></i>
                <div v-for="(value,key,index) in mess" class="item">
                    <el-input :placeholder="item[key]" type="textarea" autosize v-model="mess[key]"></el-input>
                </div>
            </div>
            <div class="wrapper" v-if="demo.length === undefined">
                <div class="item" v-for="(value,key,index) in item.mess">
                    <el-input :placeholder="key" type="textarea" autosize v-model="demo[value]"></el-input>
                </div>
            </div>
            <div v-for="(mess,demoIndex) in demo" class="wrapper" v-if="navIndex === 6" :key="demoIndex">
                <i class="el-icon-close" @click="deletItem(demoIndex)"></i>
                <div class="item">
                    <el-input v-model="mess.name" placeholder="技能"></el-input>
                    <div class="block">
                        <span class="demonstration">熟练度</span>
                        <el-slider v-model="mess.num"></el-slider>
                    </div>
                </div>
            </div>
            <el-button round v-if="item.btn" @click="addItem">{{item.btn}}</el-button>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      data: [
        { title: '基本资料', mess: { '姓名': 'name', '城市': 'city', '出生年月': 'birth', '求职意向': 'aim', '工作年限': 'workTime', '薪资要求': 'money', '学历': 'degree' } },
        { title: '工作经历', company: '公司', position: '职位', time: '时间', jobContent: '工作内容', btn: '新建一个' },
        { title: '学习经历', school: '学校', time: '在校时间', degree: '学位', btn: '新建一个' },
        { title: '项目经历', name: '项目名称', contents: '项目介绍', objlink: '链接', btn: '新建一个' },
        { title: '获得荣誉', contents: '荣誉详情', btn: '新建一个' },
        { title: '联系方式', mess: { '手机': 'phone', 'QQ': 'QQ', '微信': 'wechat', '邮箱': 'mail', '地址': 'adress' } },
        { title: '职业技能', name: '技能', btn: '新建一个' },
        { title: '自我评价', mess: { '请输入内容...': 'content' } }
      ]
    }
  },
  methods: {
    addItem: function (item) {
      let empty = {}
      this.keys.map((key) => {
        empty[key] = ''
      })
      this.demo.push(empty)
    },
    close: function () {
      this.$emit('closeDetail')
    },
    deletItem: function (index) {
      if (this.demo.length === 1) return
      this.demo.splice(index, 1)
    }
  },
  computed: {
    keys: function () {
      return Object.keys(this.demo[0])
    }
  },
  components: {},
  created () {},
  props: ['navIndex', 'demo', 'detailShow']
}
</script>
<style lang='less' scoped>
.detail{
    padding-top: 20px;
    min-width: 300px;
    position: relative;
    z-index: 2;
    i{
        position: absolute;
        right: 0;
        top: 20px;
        height: 24px;
        width: 24px;
        line-height: 22px;
        background: #ad90fc57;
        border-radius: 6px;
        transition: All 1s;
        cursor: pointer;
    }
    .el-icon-close:before{
        color: #875ff5;
        font-size: 13px;
    }
    i:hover{
        transform: rotate(180deg);
    }
    .editor{
        .title{
            font-size: 20px;
            font-weight: 700;
            text-align: left;
            color: #000000bf;
            margin-left: 20px;
        }
        .content{
            margin-top: 20px;
            .wrapper{
                padding: 15px;
                padding-left: 20px;
                padding-right: 40px;
                position: relative;
                i{
                    top: 0;
                    right: 0;
                    border-radius: 50%;
                }
                .item{
                    margin-bottom: 10px;
                    .block{
                        display: flex;
                        align-items: center;
                        .demonstration{
                            font-size: 13px;
                            margin-right: 8px;
                        }
                        .el-slider{
                            flex: 1;
                        }
                    }
                }
                .item:last-child{
                    margin-bottom:0;
                }
            }
            .wrapper:hover{
                border-left: 2px solid #AD90FC;
                background: linear-gradient(to right, #ad90fc66, #efecf552);
            }
        }
    }
}
</style>
