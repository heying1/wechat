<template>
  <div >
    <view class="userinfo">
    <view class="userinfo-avatar">
    <open-data type="userAvatarUrl"></open-data>
    </view>
    <open-data type="userNickName"></open-data>
    </view>
    <i-panel title="我要申请做教员">
      <i-input :value="name" @change="changeName($event)" title="真实姓名" autofocus placeholder="请输入真实姓名" maxlength="20" />
      <i-input :value="school" @change="changeAddress($event)" title="就读学校" placeholder="请输入学校名称" maxlength="30" />
      <i-input :value="major" @change="changeReason($event)" title="所学专业" placeholder="请输入专业名称" maxlength="50" />
       <i-input :value="intro" @change="changeReason($event)" title="自我介绍" placeholder="请介绍一下自己吧" maxlength="200" />
    </i-panel>
    <i-button @click="handleClick" type="warning" size="default">确定加入</i-button>
    <view class="tips">湖北大学家教试营中心，欢迎大家的加入！！！</view>

   
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
       name:"",
      address:"",
      reason:""
    }
  },

  components: {
    card
  },

  methods: {
     changeName (event) {
      this.name = event.mp.detail.detail.value
    },
    changeReason (event) {
      this.reason = event.mp.detail.detail.value
    },
    changeAddress (event) {
      this.address = event.mp.detail.detail.value
    },
    handleClick () {
      if (this.name && this.reason && this.address) {
        wx.showToast({
          title: '推荐了' + this.name,
          icon: 'success',
          duration: 2000
        })
        // TODO:将推荐数据提交到云数据库
      } else {
        wx.showToast({
          title: '信息不完整',
          icon: 'none',
          duration: 2000
        })
      }
    }
  },

  created () {
   
  }
}
</script>

<style scoped>
.userinfo {
  position: relative;
  width: 750rpx;
  height: 320rpx;
  color: #666;
  display: flex;
  flex-direction: column;
  align-items: center;
}
 
.userinfo-avatar {
  overflow:hidden;
  display: block;
  width: 160rpx;
  height: 160rpx;
  margin: 20rpx;
  margin-top: 50rpx;
  border-radius: 50%;
  border: 2px solid #fff;
  box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.2);
}

.tips {
  padding: 20pt;
  font-size: 10pt;
  color:darkorange;
}
</style>