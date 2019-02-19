<template>
  <div class="container-fluid">
    <link href="//vjs.zencdn.net/5.8/video-js.min.css" rel="stylesheet">
    <div class="row">
      <div class="col-md-8" id="board-remote-preview">
        <preview/>
      </div>
      <div class="col-md-4" id="board-remote-scenes">
        <ul id="scenes-list">
          <li v-for="scene in scenes" v-bind:key="scene.getName">{{scene.name}}</li>
        </ul>
      </div>
    </div>
    <div class="row" id="board-remote-commands">
      <div class="btn-group col-md-8" role="group">
        <button class="btn btn-outline-danger" v-on:click="startRecording">play</button>
        <button class="btn btn-outline-secondary" v-on:click="stopRecording">stop</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import json from '../config/config.json';
import preview from './LivePreview.vue';
import { Scene } from '@/entities/scene';

const axios = require('axios');
const apiURL = process.env.VUE_APP_API_REMOTE_URL;

@Component({
  components: {
    preview
  },
  data() {
    return {
      scenes: []
    };
  },
  methods: {
    startRecording: function() {
      axios.get(apiURL.concat(json.api_server.commands.start_recording))
        .then(alert('Recording started'))
        .catch((error: any) => alert(error));
    },
    stopRecording: function() {
      axios.get(apiURL.concat(json.api_server.commands.stop_recording))
        .then(alert('Recording stopped'))
        .catch((error: any) => alert(error));
    }
  },
  async mounted() {
    try {
      await axios.get(apiURL);
      let res2 = await axios.get(apiURL.concat((json.api_server.elements.scenes)));
      let sceneList = JSON.parse(JSON.stringify(res2.data));
      sceneList.data.forEach((scene : Scene) => {
        console.log(scene);
        this.$data.scenes.push(scene);
      });
    } catch (e) {
      throw e;
    }
  }
})

export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
