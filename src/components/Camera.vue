<template>
  <div class="hls-component">
    <video
      ref="video"
      width="100%"
      preload="auto"
      autoplay="true"
      muted="muted"
      controls
    ></video>
  </div>
</template>

<script>
import Hls from "hls.js";
export default {
  name: "Streams",
  props: {
    camera: {
      type: Object,
      required: false,
      default: () => {},
    },
  },
  mounted() {
    let video = this.$refs["video"];
    if (this.camera) {
      if (video.canPlayType("application/vnd.apple.mpegurl")) {
        video.src = this.camera.link;
      } else if (Hls.isSupported()) {
        var hls = new Hls();
        hls.loadSource(this.camera.link);
        hls.attachMedia(video);
      }
    }
  },
};
</script>
