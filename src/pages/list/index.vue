<template>
  <div>
    
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
        this.exam=res.data
      }
    )
    db.collection('music').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
      }
    )
    db.collection('sport').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
      }
    )
    db.collection('lang').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
      }
    )
    db.collection('life').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
      }
    )
    db.collection('preschool').get().then(
      res =>{
        console.log(res.data)
        this.exam=res.data
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
