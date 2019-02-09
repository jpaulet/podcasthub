<template>
  <section class="container">
    <div>
      <h1 class='title'>PodcastStash</h1>      
      <podcast v-for="(podcast, index) in podcasts" :key="`podcast-${index}`" :podcast="podcast" />
    </div>
  </section>
</template>

<script>
import Podcast from '~/components/Podcast.vue'

export default {
  components: {
    Podcast
  },
  data(){
    return {
      podcasts : null
    }
  },
  methods: {
    getPodcasts() {
      //this.podcasts = JSON.stringify(require('../data/podcasts.json'))
      this.podcasts = require('../data/podcasts.json')
    }
  },
  created(){
    this.getPodcasts();
  }

}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
