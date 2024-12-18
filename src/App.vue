<template>
    <VideoPlayer />
  </template>
  <script lang="ts">
  import { defineComponent } from 'vue';
  import VideoPlayer from './components/VideoPlayer.vue';
  export default defineComponent({
    components: {
      VideoPlayer,
    },
  });
  </script>
  <style>
  /* 你的全局样式 */
  </style>