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
      <i-grid-item @click="goList(item.url)" i-class="no-border" v-for="item in grids1" :key="item">
          <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label>{{item.type}}</i-grid-label>
      </i-grid-item> 
  </i-grid>
  <i-grid i-class="no-border">
      <i-grid-item @click="goList(item.url)" i-class="no-border" v-for="item in grids2" :key="item">
          <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label>{{item.type}}</i-grid-label>
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
      },
      grids1:[
        {type:'乐器学习',img:'/static/images/music.png',"url":'../list/main?type=1'},
        {type:'体育运动',img:'/static/images/sport.png',"url":'../list/main?type=2'},
        {type:'考试培训',img:'/static/images/exam.png',"url":'../list/main?type=3'},
        {type:'语种学习',img:'/static/images/lang.png',"url":'../list/main?type=4'}
       
      ],
      grids2:[
    
        {type:'学前小学',img:'/static/images/preschool.png',"url":'../list/main?type=5'},
        {type:'初中高中',img:'/static/images/juniorschool.png',"url":'../list/main?type=6'},
        {type:'生活兴趣',img:'/static/images/life.png',"url":'../list/main?type=7'},
        {type:'更多科目',img:'/static/images/text.png',"url":'../list/main?type=8'}
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
    goType (type) {
      let url = '../list/main?type=' + type
      mpvue.navigateTo({ url })
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