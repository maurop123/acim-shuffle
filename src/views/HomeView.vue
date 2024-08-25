<script setup>
import { computed } from 'vue'
import videos from '../data/videos.js'
console.debug('videos', videos)

const random_video_index = Math.floor(Math.random() * videos.length)
const random_video = videos[random_video_index]
console.debug('random_video', random_video)
const random_chapter_index = Math.floor(Math.random() * random_video.chapters.length)
const random_chapter = random_video.chapters[random_chapter_index]
console.debug('random_chapter', random_chapter)
const random_section_index = Math.floor(Math.random() * random_chapter.sections.length)
const random_section = random_chapter.sections[random_section_index]
if (random_chapter.sections[random_section_index + 1]) {
  const { start } = random_chapter.sections[random_section_index + 1]
  random_section.end = start
} else if (random_video.chapters[random_chapter_index + 1]) {
  const { start } = random_video.chapters[random_chapter_index + 1].sections[0]
  random_section.end = start
} else {
  random_section.end = random_video.duration
}
console.debug('random_section', random_section)
const random_time =
  Math.floor(Math.random() * (random_section.end - random_section.start)) + random_section.start
console.debug('random_time', random_time)
const sectionUri = random_section.title
  .replace(/[^a-zA-Z\s]/g, '')
  .replace(/ /g, '-')
  .toLowerCase()
console.debug('sectionUri', sectionUri)
const sections = videos.reduce((acc, video) => {
  return acc.concat(
    video.chapters.reduce((_acc, chapter) => {
      return _acc.concat(chapter.sections)
    }, [])
    /* {} //add an extra empty object between chapters to help get the right sectionUriNumber */
  )
}, [])
const sectionUriNumber =
  sections.reduce((acc, section, i) => {
    if (
      acc === null &&
      section.id === random_section.id &&
      section.title === random_section.title &&
      section.start === random_section.start
    ) {
      return { section, i }
    }
    return acc
  }, null).i + 52
console.debug('sectionUriNumber', sectionUriNumber)

function getRandomAcimYoutubeLink() {
  return `https://youtube.com/embed/${random_video.youtubeVideoId}?start=${random_time}`
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
    <h3>{{ random_chapter.title }}</h3>
    <h4>Chapter {{ random_chapter.id }}</h4>
    <h1>
      Section
      {{ random_section.id + 1 }}
    </h1>
    <!--<a
      :href="`https://acim.org/acim/chapter-${random_chapter.id}/${sectionUri}/en/s/${sectionUriNumber}`"
      target="blank"
    >-->
    <h2>{{ random_section.title }}</h2>
    <!--</a>-->
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
