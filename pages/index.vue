<template>
  <section class="container">
    <div>
      <h1 class='title'>PodcastStash</h1> 
      <div style='width:80%;margin:10px auto;text-align:right;'>        
        
        <div style='display:inline;'>
           <input type="text" placeholder="Search.." style='border-radius:6px;border:1px solid #ccc;padding:2px 5px;box-shadow:none;'>
           <fa icon="search" style='font-size:11px;color:#555;' />
        </div>
      </div>    
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
  font-size: 40px;
  color: #35495e;
  letter-spacing: 1px;
  margin-bottom:10px;
}
</style>
