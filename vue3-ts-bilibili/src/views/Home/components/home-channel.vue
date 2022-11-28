<template>

  <van-tabs v-model:active="active">
  <van-tab v-for="item in list" :title="item.text" :key="item.id"></van-tab>
  </van-tabs>

</template>

<script setup lang="ts">

import { ref } from 'vue'
import axios from 'axios'
// Ts的接口用户标记数据格式
interface INvaItem{
  id:string
  text:string
}
// ref把一个简单数据变成响应式
const active = ref(0)
const list = ref<INvaItem[]>([])

axios({
  url: '/navList',
  method: 'get'
}).then(res => {
  console.log('nav数据', res.data)
  list.value = res.data.result
})
</script>

<style>

</style>
