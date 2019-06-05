<template>
  <div>
    <view v-for="item in list" :key='item' class="top-padding">
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
  onLoad (option){/*
    console.log(option.type)
    this.list=require()*/
    
  },

  created () {
    const db = wx.cloud.database({env: 'shop-567234'})
    db.collection('exam').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
      }
    )
    db.collection('juniorschool').get().then(
      res =>{
        console.log(res.data)
        this.juniorschool=res.data
      }
    )
    db.collection('music').get().then(
      res =>{
        console.log(res.data)
        this.music=res.data
      }
    )
    db.collection('sport').get().then(
      res =>{
        console.log(res.data)
        this.sport=res.data
      }
    )
    db.collection('lang').get().then(
      res =>{
        console.log(res.data)
        this.lang=res.data
      }
    )
    db.collection('life').get().then(
      res =>{
        console.log(res.data)
        this.life=res.data
      }
    )
    db.collection('preschool').get().then(
      res =>{
        console.log(res.data)
        this.preschool=res.data
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
