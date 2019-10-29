<template>
  <card>
    {{ fullTitle }}
    <v-card-actions>
      <v-btn v-if="!isPlay" @click="play"><v-icon>mdi-play</v-icon></v-btn>
      <v-btn v-if="isPlay" @click="pause"><v-icon>mdi-pause</v-icon></v-btn>
    </v-card-actions>
  </card>
</template>

<script lang="ts">
import { Howl } from 'howler'
import {
  createComponent,
  computed,
  PropType,
  reactive,
  ref
} from '@vue/composition-api'

interface Track {
  src: string
  title: string
  author: string
}

export default createComponent({
  props: {
    track: {
      type: Object as PropType<Track>,
      required: true
    }
  },

  setup({ track }) {
    const fullTitle = computed(() => `${track.author} — ${track.title}`)
    let player: Howl | null = reactive(null)
    const isPlay = ref(false)

    const play = function() {
      if (!player) {
        player = new Howl({
          src: track.src
        })
      }

      player.play()
      isPlay.value = true
    }

    const pause = function() {
      if (player) {
        player.pause()
        isPlay.value = false
      }
    }

    return {
      fullTitle,
      isPlay,
      play,
      pause
    }
  }
})
</script>
