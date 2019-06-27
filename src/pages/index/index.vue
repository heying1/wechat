<template>
  <div>
    <swiper
      :indicator-dots="indicatorDots"
      :autoplay="autoplay"
      :interval="interval"
      :duration="duration"
      style="height:200px"
    >
    <block v-for="item in imgUrls" :key="item">
      <swiper-item>
        <image :src="item" style="width:100%;"/>
      </swiper-item>
    </block>
  </swiper>
    <i-notice-bar icon="systemprompt" loop>
    好好学习，天天向上！
    </i-notice-bar>
      <Page :id="pageId" show-total :total="total" :page-size="pagesize"></Page>
      <i-button @click="goElevatorPage" type="success" >教员库</i-button>
       <i-button @click="handleClick" type="success" >学员库</i-button>
       <i-grid i-class="no-border">
      <i-grid-item @click="goType(type)" i-class="no-border" v-for="item in grids1" :key="item">
          <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label>{{item.type}}</i-grid-label>
      </i-grid-item> 
  </i-grid>
  <i-grid i-class="no-border">
      <i-grid-item @click="goType(type)" i-class="no-border" v-for="item in grids2" :key="item">
          <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label>{{item.type}}</i-grid-label>
      </i-grid-item>
  </i-grid>

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
import card from '@/components/card'

export default {
  data () {
    return {
      list:[],
      /*
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },*/
       imgUrls: [
        '/static/images/1.jpg',
        '/static/images/2.jpg',
        '/static/images/3.jpg'
      ],
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      grids1:[
        {type:'乐器学习',img:'/static/images/music.png',"url":'../list/main?type=music'},
        {type:'体育运动',img:'/static/images/sport.png',"url":'../list/main?type=sport'},
        {type:'考试培训',img:'/static/images/exam.png',"url":'../list/main?type=exam'},
        {type:'语种学习',img:'/static/images/lang.png',"url":'../list/main?type=lang'}
       
      ],
      grids2:[
    
        {type:'学前小学',img:'/static/images/preschool.png',"url":'../list/main?type=preschool'},
        {type:'初中高中',img:'/static/images/juniorschool.png',"url":'../list/main?type=juniorschool'},
        {type:'生活兴趣',img:'/static/images/life.png',"url":'../list/main?type=life'},
        {type:'更多科目',img:'/static/images/text.png',"url":'../list/main?type=text'}
      ],
      pageId:"logs",
      pageId1:"index"
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
    goType (type) {
      console.log(type)
      let url = '../list/main?type=' + type
      mpvue.navigateTo({ url })
    },
    goElevatorPage(){
      wx.navigateTo({
        url:'../teacher/main' 
        })  
   },
   handleClick(){
     wx.navigateTo({
       url:'../student/main'
     })
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
    db.collection('exam').get().then(
      res =>{
        console.log(res.data)
        this.exam = res.data
      }
    )
    db.collection('juniorschool').get().then(
      res =>{
        console.log(res.data)
        this.juniorschool= res.data
      }
    )
    db.collection('music').get().then(
      res =>{
        console.log(res.data)
        this.music = res.data
      }
    )
    db.collection('sport').get().then(
      res =>{
        console.log(res.data)
        this.sport = res.data
      }
    )
    db.collection('lang').get().then(
      res =>{
        console.log(res.data)
        this.lang = res.data
      }
    )
    db.collection('life').get().then(
      res =>{
        console.log(res.data)
        this.life = res.data
      }
    )
    db.collection('preschool').get().then(
      res =>{
        console.log(res.data)
        this.preschool = res.data
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