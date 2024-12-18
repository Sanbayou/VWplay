<template>
  <div class="video-player">
    <input 
      type="file" 
      @change="handleFileSelect" 
      accept="video/*"
      class="file-input"
    />
    <video 
      ref="videoElement" 
      @timeupdate="onTimeUpdate" 
      controls
      v-if="videoUrl"
    >
      <source :src="videoUrl" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
    <Danmaku :currentTime="currentTime" />
    <SubtitleDisplay :currentTime="currentTime" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Danmaku from './Danmaku.vue';
import SubtitleDisplay from './SubtitleDisplay.vue';

export default defineComponent({
  components: { Danmaku, SubtitleDisplay },
  setup() {
    const videoElement = ref<HTMLVideoElement | null>(null);
    const currentTime = ref(0);
    const videoUrl = ref<string>('');

    const handleFileSelect = (event: Event) => {
      const input = event.target as HTMLInputElement;
      if (input.files && input.files[0]) {
        const file = input.files[0];
        videoUrl.value = URL.createObjectURL(file);
        
        // 获取视频文件所在目录的同名字幕文件
        const fileName = file.name;
        const baseName = fileName.substring(0, fileName.lastIndexOf('.'));
        console.log('Looking for subtitle file:', baseName + '.srt');
      }
    };

    const onTimeUpdate = () => {
      if (videoElement.value) {
        currentTime.value = videoElement.value.currentTime;
      }
    };

    return { 
      videoElement, 
      currentTime, 
      videoUrl,
      handleFileSelect,
      onTimeUpdate 
    };
  },
});
</script>

<style scoped>
.video-player {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.file-input {
  margin-bottom: 1rem;
  padding: 0.5rem;
  width: 100%;
}

video {
  width: 100%;
  background: #000;
}
</style>