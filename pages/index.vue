<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-card>
        <player :track="track" />
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script lang="ts">
import Vue from 'vue'
import Player from '@/components/player'

export default Vue.extend({
  components: { Player },

  data() {
    return {
      track: {
        src: '/brobob.mp3',
        title: 'Track',
        author: 'Author'
      }
    }
  }
})
</script>
