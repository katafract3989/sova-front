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
  async mounted() {
    console.log(this.camera);
    if (this.camera) {
      let hls = new Hls();
      let stream = this.camera.link;
      let video = this.$refs["video"];
      await hls.loadSource(stream);
      await hls.attachMedia(video);
    }
  },
};
</script>
