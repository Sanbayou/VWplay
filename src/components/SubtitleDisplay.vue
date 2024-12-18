<template>
    <div class="subtitle-display">
      <p v-if="currentSubtitle">{{ currentSubtitle }}</p>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref, watch } from 'vue';
  
  export default defineComponent({
    props: {
      currentTime: {
        type: Number,
        required: true,
      },
    },
    setup(props) {
      const currentSubtitle = ref<string | null>(null);
  
      watch(
        () => props.currentTime,
        (newTime) => {
          // 这里应该有逻辑来匹配当前时间的字幕
          // currentSubtitle.value = matchedSubtitle;
        }
      );
  
      return { currentSubtitle };
    },
  });
  </script>
  
  <style scoped>
  .subtitle-display {
    position: absolute;
    bottom: 20px;
    width: 100%;
    text-align: center;
    color: white;
    background-color: rgba(0, 0, 0, 0.5);
  }
  </style>