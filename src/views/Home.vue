<template>
  <div class="container col-md-6">
    <img alt="Vue logo" src="../assets/logo.png">
    <div class="card">
      <div class="card-header">OBS REMOTE WEB-APP</div>
      <div class="card-body">
        <Board/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Board from '@/components/Board.vue'; // @ is an alias to /src

@Component({
  components: {
    Board
  },
  data: function() {
    return {
      env: process.env.NODE_ENV
    };
  }
})
export default class Home extends Vue {}
</script>
