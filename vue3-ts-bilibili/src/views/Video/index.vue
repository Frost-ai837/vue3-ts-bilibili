<!-- eslint-disable vue/multi-word-component-names -->
<template>
 <!-- 头部组件 -->
 <AppHeader/>
  <!-- 视频播放 -->
  <VideoPlay :videoInfo="videoInfo" />
  <!-- 视频详情 -->
  <VideoInfo :videoInfo="videoInfo" />
  <!-- 相关推荐/评论 -->
  <VideoBottom />
</template>

<script setup lang="ts">
import AppHeader from '@/components/app-header.vue'
import axios from 'axios'
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import VideoPlay from './component/video-play.vue'
import VideoInfo from './component/video-info.vue'
import VideoBottom from './component/video-bottom.vue'

export interface IVideoItem{
  author?: string
  authorIconSrc?: string
  commentCount?: number
  date?: string
  id?: string
  poster?: string
  playCount?: string
  likeCount?: string
  favCount?: string
  videoSrc?: string
  videoTitle?: string

}

const videoInfo = ref<IVideoItem>({})
const route = useRoute()

axios({
  url: '/videoDetail',
  method: 'get',
  params: { id: route.params.id }
}).then(({ data }) => {
  videoInfo.value = data.result
  console.log('视频详情的数据', data.result)
})
</script>

<style lang="less" scoped>
.video-info {
  padding: 3vw 2vw;
  border-bottom: 1px solid #ddd;
  .title {
    font-size: 4vw;
    line-height: 6vw;
    margin: 3vw 0;
  }
  .author-info {
    display: flex;
    align-items: center;
    font-size: 3vw;
    color: #999;
    .author {
      flex: 1;
      .author-avatar {
        width: 5vw;
        height: 5vw;
        object-fit: cover;
        border-radius: 50%;
        overflow: hidden;
        margin: 0 1vw;
        background: url(~@/assets/images/loading.png) no-repeat center #e7e7e7;
      }

      .author-name {
        color: #212121;
      }
    }
    > span {
      margin: 0 2vw;
    }
    .iconfont {
      font-size: 5vw;
      color: #757575;
      margin-right: 2vw;
    }
  }
}
</style>
