<template>
  <div class="container">
    <!-- 头部 -->
    <div class="head">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <span class="head-info">消息</span>
    </div>
    <!-- 搜索 -->
    <div class="search">
      <input type="search"/>
      <span>搜索</span>
    </div>
    <!-- 内容 -->
    <div class="infoAll" v-for="(item,index) in commitInfo" :key="index">
      <!-- {{item.img}} -->
      <ul>
        <li @touchstart="touchStart($event)" @touchend="touchEnd($event,index)" :data-type="item.type">
          <div class="imgInfo" @click="recover(index)">
            <img :src="item.img">
          </div>
          <div class="centerInfo">
            <div class="name">
               <span>{{item.name}}</span>
            </div>
            <div class="sonName">
              <span>{{item.sonName}}</span>
              </div>
          </div>
          <div class="timeInfo" @click="recover(index)">
            <div class="time">
              <text>{{item.time}}</text>
            </div>
            <div class="infoNum" style="">
                <text style="font-size:12px;">{{item.infoNum}}</text>  
            </div>
          </div>
          <div class="top">
            置顶
          </div>
          <div class="delect">
            删除
          </div>
        </li>
        
      </ul>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      userInfo: {},
      commitInfo:[
        {
          img:"http://img3.imgtn.bdimg.com/it/u=3067730600,935028889&fm=27&gp=0.jpg",
          name:"旺财",
          sonName:"今晚去吃饭吗?",
          time:"19:08",
          infoNum:"9",
          top:false,
          type:0
        },

        {
          img:"http://img1.imgtn.bdimg.com/it/u=1257196754,3171363795&fm=27&gp=0.jpg",
          name:"前端学习群",
          sonName:"hanber：异步与同步的问题",
          time:"02:08",
          infoNum:"99+",
          top:false,
          type:0
        },
        {
          img:"https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1672209094,624238697&fm=27&gp=0.jpg",
          name:"小学同学",
          sonName:"好久不见，最近好吗？",
          time:"02:08",
          infoNum:"9",
          top:false,
          type:0
        },
         {
          img:"https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1312347818,1612941824&fm=200&gp=0.jpg",
          name:"老妈",
          sonName:"啥时候回家一趟呀？",
          time:"23:08",
          infoNum:"1",
          top:false,
          type:0
        },
        {
          img:"http://img2.imgtn.bdimg.com/it/u=1093392508,3329264726&fm=27&gp=0.jpg",
          name:"AD动漫群",
          sonName:"ghost:《你的名字》求资源",
          time:"02:08",
          infoNum:"99+",
          top:false,
          type:0
        }
      ]
    }
  },

  components: {
    card
  },

  methods: {
  // 滑动开始
    touchStart(e){
      // 获取移动距离，可以通过打印出e，然后分析e的值得出
        this.startX = e.mp.changedTouches[0].clientX;
    },
    // 滑动结束
    touchEnd(e,index){
        // 获取移动距离
        this.endX = e.mp.changedTouches[0].clientX;  
        if(this.startX-this.endX > 10){
            for(let i=0;i<this.commitInfo.length;i++){
                  this.commitInfo[i].type = 0
            }
            this.commitInfo[index].type = 1
        }
        else if(this.startX-this.endX < -10){
            for(let i=0;i<this.commitInfo.length;i++){
                  this.commitInfo[i].type = 0
            }
        }
    
    },
    // 点击回复原状
    recover(index){
          this.commitInfo[index].type = 0
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>
<style>
  page{
    background-color: #fff;
    width: 100%;
  }
</style>

<style lang="sass" scoped>
  @import './index'
</style>

