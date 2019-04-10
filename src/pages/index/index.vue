<template>
  <div>
    <i-notice-bar>
    好好学习，天天向上！
    </i-notice-bar>
    <i-grid i-class="no-border">
    <i-grid-item>  
         <i-grid-icon>
            <image src="/static/images/music.png" />
        </i-grid-icon> 
         <i-grid-label>乐器学习</i-grid-label>
    </i-grid-item>

    <i-grid-item>  
         <i-grid-icon>
            <image src="/static/images/sport.png" />
        </i-grid-icon> 
         <i-grid-label>体育运动</i-grid-label>
    </i-grid-item>
     
</i-grid>
<i-grid i-class="no-border">
    <i-grid-item>  
         <i-grid-icon>
            <image src="/static/images/exam.png" />
        </i-grid-icon> 
         <i-grid-label>考试培训</i-grid-label>
    </i-grid-item>
    <i-grid-item>  
         <i-grid-icon>
            <image src="/static/images/lang.png" />
        </i-grid-icon> 
         <i-grid-label>语种学习</i-grid-label>
    </i-grid-item>
</i-grid>
<view v-for="item in data" :key='item' class="top-padding">
 <i-card title="卡片标题" extra="额外内容" thumb="https://i.loli.net/2017/08/21/599a521472424.jpg">
    <view slot="content">内容不错</view>
    <view slot="footer">尾部内容</view>
</i-card>
</view>
<i-card title="卡片标题" extra="额外内容" thumb="https://i.loli.net/2017/08/21/599a521472424.jpg">
    <view slot="content">内容不错</view>
    <view slot="footer">尾部内容</view>
</i-card>
<i-card title="卡片标题" extra="额外内容" thumb="https://i.loli.net/2017/08/21/599a521472424.jpg">
    <view slot="content">内容不错</view>
    <view slot="footer">尾部内容</view>
</i-card>  

  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
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
        this.data=res.data
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
</style>