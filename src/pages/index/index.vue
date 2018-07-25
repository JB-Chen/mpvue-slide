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
        <li>
          <div class="imgInfo">
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
        
          <span class="time">{{item.time}}</span>
          <div class="infoNum" style="height: 30rpx;border-radius: 10rpx;background-color: #93D5ED;display:flex;align-items:center; justify-content:center;">
            <text style="font-size:12px;">{{item.infoNum}}</text>  
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
          top:false
        },
        {
          img:"http://img2.imgtn.bdimg.com/it/u=1093392508,3329264726&fm=27&gp=0.jpg",
          name:"AD动漫群",
          sonName:"ghost:《你的名字》求资源！",
          time:"02:08",
          infoNum:"99+",
          top:false
        },
        
      ]
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
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
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
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

