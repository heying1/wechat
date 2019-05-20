<template>
  <div>
    <Table :columns="columns1" :data="list"></Table>
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
      columns1:  [ // 表头定义
               {
                     title: '全部',
                     key: ''  // 对应list的name
                },
                {
                  title:'学前小学',
                  key:''
                },
                {
                  title:'初中高中',
                  key:''
                },
                {
                  title:'乐器学习',
                  key:''
                },
                {
                  title:'生活兴趣',
                  key:''
                },
                {
                  title:'语种学习',
                  key:''
                },
                {
                  title:'体育运动',
                  key:''
                },
                {
                  title:'考试培训',
                  key:''
                },
          ]
    }
  },

  created () {
    
  }
}
</script>

<style>

</style>
