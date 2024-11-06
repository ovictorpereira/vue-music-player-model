<template>
  <MusicPlayer :playlist="playlist" />
</template>

<script setup lang="ts">
import MusicPlayer from '@/components/MusicPlayer.vue'

const playlist = [
  {
    id: 1,
    albumCover:
      'https://cdns-images.dzcdn.net/images/cover/de9496f611d6d7391fa57401bac99d5b/0x1900-000000-80-0-0.jpg',
    musicName: 'Born to die',
    artistName: 'Lana del Rey',
    duration: 192,
  },
  {
    id: 2,
    albumCover: 'https://pure-music.co.uk/wp-content/uploads/2019/04/Thriller-Album-Cover.png',
    musicName: 'Thriller',
    artistName: 'Michael Jackson',
    duration: 210,
  },
]
</script>
