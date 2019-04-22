<template>
  <div>
    <i-notice-bar icon="systemprompt" loop>
    好好学习，天天向上！
    </i-notice-bar>

    <i-row i-class="have-border">
    <i-col span="8" i-class="have-border" offset="4">
      col-8
      <i-button bind:click="handleClick" type="success" shape="circle">默认尺寸</i-button>

    </i-col>

    <i-col span="8" i-class="have-border" offset="4">
      col-8
      <i-button bind:click="handleClick" type="success" shape="circle">默认尺寸</i-button>


      

    </i-col>
    </i-row>

    <i-grid i-class="no-border">
    <i-grid-item i-class="no-border">  
         <i-grid-icon>
            <image src="/static/images/music.png" />
        </i-grid-icon> 
         <i-grid-label>乐器学习</i-grid-label>
    </i-grid-item>

    <i-grid-item i-class="no-border">  
         <i-grid-icon>
            <image src="/static/images/sport.png" />
        </i-grid-icon> 
         <i-grid-label>体育运动</i-grid-label>
    </i-grid-item> 
</i-grid>

<i-grid i-class="no-border">
    <i-grid-item i-class="no-border">  
         <i-grid-icon>
            <image src="/static/images/exam.png" />
        </i-grid-icon> 
         <i-grid-label>考试培训</i-grid-label>
    </i-grid-item>
    <i-grid-item i-class="no-border">  
         <i-grid-icon>
            <image src="/static/images/lang.png" />
        </i-grid-icon> 
         <i-grid-label>语种学习</i-grid-label>
    </i-grid-item>
</i-grid>

<view v-for="item in list" :key='item' class="top-padding">
 <i-card :title="item.name" :extra="item.id" :thumb="item.photo">
    <view slot="content">{{item.major}}</view>
    <view slot="content">{{item.school}}</view>
    <view slot="content">{{item.intro}}</view>
    <view slot="footer"></view>
</i-card>
</view>

  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      list:[],
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    // let app = getApp()
    const db = wx.cloud.database({env: 'shop-567234'})
    db.collection('data').get().then(
      res =>{
        console.log(res.data)
        this.list=res.data
      }
    )
    wx.cloud.callFunction({name: 'user'}).then(
      res => {console.log(res)}
    )
  }
}
</script>

<style scoped>
div >>>.no-border{
  border-width: 0pt;
}
div >>>.have-border{
  border-width: 1pt;
}
</style>