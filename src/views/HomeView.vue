<script setup lang="ts">
import { computed } from 'vue'
import chapters from '../data/chapters.js'
console.debug('chapters', chapters)

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

const random_video_index = Math.floor(Math.random() * 1) //videos.length)
const random_video = videos[random_video_index]
const random_time = Math.floor(Math.random() * random_video.duration)

function getRandomAcimYoutubeLink() {
  return `${random_video.link}?start=${random_time}`
}

const randomChapter = computed(() => {
  const randTime = random_time
  const chosenSection = chapters.reduce((acc, chapter, i, arr) => {
    const { sections } = chapter
    const _chosenSection = sections.reduce((add, section, j, ass) => {
      if (section.start > randTime) return section
      else return add
    }, null)
    if (_chosenSection !== null) {
      chapter.section = _chosenSection
      return chapter
    } else return acc
    /* console.debug('randTime', randTime, 'time.start', section.start) */
    /* if (randTime > section.start) return _arr[j + 1] */
    /* if (randTime < section.start) return _acc */
    /* }, _arr[0]) */
  }, null)
  console.debug('chosenSection', chosenSection)
  return chosenSection
})

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
    <h3>{{ randomChapter.title }}</h3>
    <h4>Chapter {{ randomChapter.id }}</h4>
    <h1>
      Section
      {{ randomChapter.section.id }}
    </h1>
    <h2>{{ randomChapter.section.title }}</h2>
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
  color: #dfa013 !important;
  font-family: 'Playfair Display' !important;
}

h1 {
  font-size: 2rem;
  align-self: start;
}

h2 {
  font-size: 3rem;
  text-align: center;
}

h3 {
  font-size: 1.5rem;
  align-self: end;
}

h4 {
  font-size: 1.2rem;
  align-self: end;
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
