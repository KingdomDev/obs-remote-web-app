<template>
  <video id="player-preview" controls preload="none" autoplay>
    <source :src="live_url" type="application/vnd.apple.mpegurl">
  </video>
  <!--custom-video id="player-preview" class="vjs-default-skin" controls>
    <source
      :src="live_url"
      type="application/x-mpegURL">
  </custom-video-->
</template>

<script>
import { customVideo } from '@videojs/http-streaming/dist/videojs-http-streaming.min';

export default {
  name: 'LivePreview',
  components: {
  },
  data: function() {
    return {
      live_url: process.env.VUE_APP_PREVIEW_URL
    };
  },
  mounted() {
    // var player = videojs('player-preview')
    // player.play()
  }
};
</script>

<style scoped>
  #player-preview {
    width: 90%;
    height: 90%;
  }
</style>
