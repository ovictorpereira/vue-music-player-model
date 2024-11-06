<template>
  <div class="vplayer-card">
    <img
      class="album-cover"
      :src="props.playlist[playlistIndex].albumCover"
      alt="music album cover"
    />

    <h2 class="music-name">{{ props.playlist[playlistIndex].musicName }}</h2>
    <h3 class="artist-name">{{ props.playlist[playlistIndex].artistName }}</h3>

    <div class="vplayer-control">
      <div class="control-btn">
        <img
          src="@/assets/icon-player-left.svg"
          alt="jump to previous music"
          @click="previousMusic()"
        />
      </div>

      <div class="control-btn">
        <img src="@/assets/player-play.svg" alt="play" />
      </div>

      <div class="control-btn">
        <img src="@/assets//icon-player-right.svg" alt="jump to next music" @click="nextMusic()" />
      </div>
    </div>

    <ProgressBar
      :progress="percentage(musicPlayTime, props.playlist[playlistIndex].duration)"
      @change="updateMusicPosition"
    />

    <div class="vplayer-time-container">
      <p>{{ formatDuration(musicPlayTime) }}</p>
      <p>{{ formatDuration(props.playlist[playlistIndex].duration) }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { MusicInterface } from '@/types/Music'
import { ref } from 'vue'
import ProgressBar from './ProgressBar.vue'

const props = defineProps<{
  playlist: MusicInterface[]
}>()

const playlistIndex = ref<number>(0)

const musicPlayTime = ref<number>(100)

const updateMusicPosition = (e: number): void => {
  musicPlayTime.value = Math.round(
    reversePercentage(e, props.playlist[playlistIndex.value].duration),
  )
}

const nextMusic = (): void => {
  musicPlayTime.value = 0
  if (playlistIndex.value < props.playlist.length - 1) playlistIndex.value++
  else playlistIndex.value = 0
}

const previousMusic = (): void => {
  musicPlayTime.value = 0
  if (playlistIndex.value > 0) playlistIndex.value--
  else playlistIndex.value = props.playlist.length - 1
}

const formatDuration = (time: number): string => {
  const minutes = Math.floor(time / 60)
  const seconds = time - minutes * 60
  return `${minutes}:${seconds.toString().padStart(2, '0')}`
}

const percentage = (partialValue: number, totalValue: number) => (100 * partialValue) / totalValue
const reversePercentage = (percentage: number, totalValue: number) =>
  (percentage / 100) * totalValue
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto:100,200,300,400,500,600');

.vplayer-card {
  background-color: #2a2141;
  width: 100%;
  max-width: 260px;
  border-radius: 9px;
  padding: 36px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  font-family: 'Roboto', serif;
  font-weight: 400;
  font-style: normal;
  color: #e1e1e6;
}

.vplayer-card .album-cover {
  width: 190px;
  height: 190px;
  border-radius: 9px;
  object-fit: cover;
  margin-bottom: 29px;
  align-self: center;
}

.vplayer-card .music-name {
  font-weight: 700;
  font-size: 24px;
  margin: 0 0 10px 0;
}

.vplayer-card .artist-name {
  font-size: 19px;
  margin: 0 0 29px 0;
}

.vplayer-control {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 29px;
}

.vplayer-control .control-btn {
  width: 29px;
  height: 29px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.vplayer-control .control-btn:hover {
  opacity: 0.8;
}

.vplayer-time-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
