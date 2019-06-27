<template>
  <div>
    
    <Page :id="pageId" show-total :total="total" :page-size="pagesize"></Page>

<view v-for="item in student" :key='item' class="top-padding">
 <i-card :title="item.name" :extra="item.id" >
    <view slot="content">就读年级：{{item.grade}}</view>
    <view slot="content">需辅导科目{{item.major}}</view>
    <view slot="content">介绍：{{item.intro}}</view>
    <view slot="content">对教员要求：{{item.need}}</view>
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
      student:[
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
    
    db.collection('student').get().then(
      res =>{
        console.log(res.data)
        this.student=res.data
        
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