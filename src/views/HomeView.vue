<script setup lang="ts">
import { ref } from 'vue'

const videos = [
  {
    id: 1,
    duration: 31676,
    link: 'https://www.youtube.com/embed/5hWJN4J-nyI',
    time: 60 * 60 * 8 + 60 * 47 + 56
  },
  {
    id: 2,
    time: 60 * 60 * 9 + 60 * 3 + 42,
    link: 'https://www.youtube.com/embed/hke9xRWiVZw'
  },
  {
    id: 3,
    time: 60 * 60 * 10 + 60 * 49 + 49,
    link: 'https://www.youtube.com/embed/GBrh2bXrwZg'
  },
  {
    id: 4,
    time: 60 * 60 * 8 + 60 * 45 + 16,
    link: 'https://www.youtube.com/embed/16TlrcW3eGI'
  }
]

const chapters = [
  {
    id: 1,
    link: videos[0].link,
    start: 1342
  },
  {
    id: 2,
    link: videos[0].link,
    start: 4279
  },
  {
    id: 3,
    link: videos[0].link,
    start: 8205
  },
  {
    id: 4,
    link: videos[0].link,
    start: 11532
  },
  {
    id: 5,
    link: videos[0].link,
    start: 15716
  },
  {
    id: 6,
    link: videos[0].link,
    start: 19054
  },
  {
    id: 7,
    link: videos[0].link,
    start: 22750
  },
  {
    id: 8,
    link: videos[0].link,
    start: 27617
  }
]

const random_video_index = Math.floor(Math.random() * videos.length)
const random_video = videos[random_video_index]
const random_time = Math.floor(Math.random() * random_video.duration)

function getRandomAcimYoutubeLink() {
  return `${random_video.link}?start=${random_time}`
}

function randomInteger(topNumber) {
  return Math.floor(Math.random() * topNumber) + 1
}

function arrayRandomItem(arr) {
  const randomIndex = Math.floor(Math.random() * arr.length)
  return arr[randomIndex]
}
</script>

<template>
  <main>
    <iframe
      class="responsive-iframe"
      :src="getRandomAcimYoutubeLink()"
      title="ACIM video player"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    ></iframe>
  </main>
</template>

<style>
body {
  background: #170a3d !important;
}

html,
body,
#app,
main {
  height: 100%;
}

html {
  font-size: 20px;
}

@media only screen and (max-width: 768px) {
  /* medium */
  html {
    font-size: 15px;
  }
}

@media only screen and (max-width: 560px) {
  /* small */
  html {
    font-size: 10px;
  }
}
</style>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.responsive-iframe {
  width: 30rem;
  height: 25rem;
}
</style>
