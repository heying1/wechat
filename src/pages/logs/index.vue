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
