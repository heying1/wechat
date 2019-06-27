<template>
  <div>
    
    <Page :id="pageId" show-total :total="total" :page-size="pagesize"></Page>

<view v-for="item in list" :key='item' class="top-padding">
 <i-card :title="item.name" :extra="item.id" :thumb="item.photo">
    <view slot="content">{{item.school}}</view>
    <view slot="content">{{item.major}}</view>
    <view slot="content">{{item.intro}}</view>
    <view slot="footer"></view>
</i-card>
</view>
<view v-for="item in teacher" :key='item' >
 <i-card :title="item.name" :extra="item.id" :thumb="item.photo">
    <view slot="content">{{item.school}}</view>
    <view slot="content">{{item.major}}</view>
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
      teacher:[
      ],
      
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
    },
    goList (url) {
      mpvue.navigateTo({ url })
    },
    
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
    db.collection('teacher').get().then(
      res =>{
        console.log(res.data)
        this.teacher=res.data
        
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