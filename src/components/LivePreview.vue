<template>
  <div class="columns">
    <div class="column is-8 is-offset-1">
      <video id="player-preview" autoplay>
        <source :src="live_url" type="application/x-mpegURL">
      </video>
    </div>
    <div class="column is-2" id="board-remote-scenes">
      <b-table :data="scenes" :columns="columns">
      </b-table>
    </div>
  </div>
</template>

<script>
import videojs from 'video.js';
import 'videojs-contrib-hls';
import { Scene } from '@/entities/scene';
import json from '../config/config.json';

const axios = require('axios');
const apiURL = process.env.VUE_APP_API_REMOTE_URL;

export default {
  name: 'LivePreview',
  components: {
  },
  data: function() {
    return {
      live_url: process.env.VUE_APP_PREVIEW_URL,
      scenes: [],
      columns: [
        {
          field: 'name',
          label: 'Scènes'
        }
      ]
    };
  },
  async mounted() {
    try {
      await axios.get(apiURL);
      let res2 = await axios.get(apiURL.concat((json.api_server.elements.scenes)));
      let sceneList = JSON.parse(JSON.stringify(res2.data));
      var player = videojs('player-preview');
      sceneList.data.forEach(scene => {
        // console.log(scene);
        this.$data.scenes.push(scene);
      });
    } catch (e) {
      throw e;
    }
  }
};
</script>

<style scoped>
  #player-preview {
    width: 100%;
    height: 100%;
  }
  #scenes-list {
    height: 120px;
    overflow-y: scroll;
  }
</style>
