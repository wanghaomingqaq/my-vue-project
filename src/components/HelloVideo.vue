<template>
  <div class="video-container">
    <video ref="video" width="640" height="480" autoplay></video>
    <button class="fullscreen-button" @click="goFullScreen">
      <el-icon size="20"><FullScreen /></el-icon>
    </button>
  </div>
</template>

<script>
export default {
  name:"HelloVideo",
  mounted() {
    this.getVideo();
  },
  methods: {
    async getVideo() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ video: true });
        this.$refs.video.srcObject = stream;
      } catch (err) {
        console.error("Error accessing the camera", err);
      }
    },
    goFullScreen() {
      const videoElement = this.$refs.video;
      if (videoElement.requestFullscreen) {
        videoElement.requestFullscreen();
      } else if (videoElement.mozRequestFullScreen) { /* Firefox */
        videoElement.mozRequestFullScreen();
      } else if (videoElement.webkitRequestFullscreen) { /* Chrome, Safari & Opera */
        videoElement.webkitRequestFullscreen();
      } else if (videoElement.msRequestFullscreen) { /* IE/Edge */
        videoElement.msRequestFullscreen();
      }
    },
  }
}
</script>
<style scoped>
.video-container {
  position: relative;
}

.fullscreen-button {
  position: absolute;
  right: 10px;  /* 右下角定位 */
  bottom: 10px;
  background: transparent;
  border: none;
  cursor: pointer;
}
</style>