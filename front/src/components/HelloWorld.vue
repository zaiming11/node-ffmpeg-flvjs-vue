<template>
  <div>
    <video class="demo-video" ref="player" muted autoplay></video>
  </div>
</template>
<script>
import flvjs from "flv.js";
export default {
  data() {
    return {
      id: "1",
      rtsp: "rtsp://admin:246810lzb@192.168.16.4:554/Streaming/Channels/301?transportmode=unicast",
      player: null,
    };
  },
  mounted() {
    if (flvjs.isSupported()) {
      let video = this.$refs.player;
      if (video) {
        this.player = flvjs.createPlayer({
          type: "flv",
          isLive: true,
          url: `ws://localhost:8888/rtsp/${this.id}/?url=${this.rtsp}`,
        });
        this.player.attachMediaElement(video);
        try {
          this.player.load();
          this.player.play();
        } catch (error) {
          console.log(error);
        }
      }
      // if (video) {
      //     this.player = flvjs.createPlayer({
      //         type: "flv",
      //         url: `/static/test.flv`
      //     });
      //     this.player.attachMediaElement(video);
      //     try {
      //         this.player.load();
      //         this.player.play();
      //     } catch (error) {
      //         console.log(error);
      //     };
      // }
    }
  },
  beforeDestroy() {
    this.player.destory();
  },
};
</script>
<style>
.demo-video {
  max-width: 880px;
  max-height: 660px;
}
</style>