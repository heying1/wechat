<template>
  <div>
    <i-panel title="具体科目">
      <view>
        <i-card i-class="split" v-for="item in recommand" :key="item" :extra="item.name" :thumb="item.img">
            <view slot="content">{{item.school}}</view>
            <view slot="content">{{item.major}}</view>
            <view slot="content">{{item.intro}}</view>
            <view slot="footer"></view>
        </i-card>
      </view>
    </i-panel>
  </div>
</template>

<script>


export default {

  data () {
    return {
      recommand: []
    }
  },

  onLoad (option){
    console.log(option.type)
    this.recommand = require('@/data/' + option.type + '.json')
  },

  created () {
  }
}
</script>

<style scoped>
div >>> .split {
  margin-bottom: 10pt;
}
</style>
