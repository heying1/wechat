<template>
  <div>
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
import { formatTime } from '@/utils/index'
import card from '@/components/card'

export default {
  components: {
    card
  },

  data () {
    return {
      logs: [],
      
    }
  },
  onLoad (option){
    console.log(option)
    
  },

  created () {
    const db = wx.cloud.database({env: 'shop-567234'})
    db.collection('option.type').get().then(
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

<style>

</style>
