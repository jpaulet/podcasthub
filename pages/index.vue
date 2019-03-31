<template>
  <section class="container">
    <div id='mainPage' style='height:100%;width:100%;overflow: hidden;'>
      <div class='row headerBanner'>  
        <h1 class="title col-xs-12 col-sm-6">
          podcastStash 
          <fa icon='microphone-alt' />
        </h1>

        <div class='headerButtons hidden-xs col-sm-6' style='padding:30px 10px;text-align: right;'>
          <a href='https://jpaulet.typeform.com/to/TJOlbG' target='_blank' class='bmc-button' style='font-size:11px;text-decoration: none;margin-right:8px !important;vertical-align:top;'>Add Podcast</a>

          <link href="https://fonts.googleapis.com/css?family=Lato&subset=latin,latin-ext" rel="stylesheet">
          <a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/mpSEk0R">
            <img src="https://www.buymeacoffee.com/assets/img/BMC-btn-logo.svg" alt="Support My Work" style='height:20px;margin-top:3px;'>
            <span style="margin-left:5px;">Support My Work</span>
          </a>
        </div> 
      </div>

      <div class='textWrapper col-xs-12' style='margin-top:15px;margin-bottom:25px;line-height:22px;'> 
        <span style='text-decoration: underline;'>Hand-picked</span> list with <span style='font-size:16px;background-color: rgba(255, 255, 255, 0.19);border-radius:6px;padding:3px 6px;'>+{{ podcasts.length }}</span> awesome podcasts for makers, designers, programmers & more! <fa icon='microphone-alt' />
      </div>

      <div class='filterList' style='padding:10px 20px 30px;'>
        <button class='filterTagButton col-xs-4 col-md-2' @click='showTags = !showTags'>Filter Tags</button>

        <div class='searchBox col-xs-8 col-sm-5 col-sm-offset-2 col-lg-offset-5' style='text-align:right;float:right;'>
          <input class='searchInput' type="text" placeholder="Search.." v-model="search" />
          <fa class='searchIcon' icon="search" v-if='!search' />
          <fa class='searchIcon' icon="times" v-if='search' @click='cleanSearch' />
        </div>
        
        <div class='filterTags' v-if='showTags'> 
          <button class='closeButton' @click='showTags = false'> x </button>       
          <b-form-checkbox-group buttons
            v-model='selectedTags' 
            name="check-button" 
            class='tagCheckbox'
            :options='filterTags'
          >
            {{tag}}
          </b-form-checkbox-group>
        </div> 
      </div>

      <div class='podcastsBox' style='margin-bottom:80px;clear:both;'>
        <podcast v-for="(podcast, index) in filteredItems" :key="`podcast-${index}`" :podcast="podcast"/>
        <div v-if='!filteredItems.length' style='height:80vh;clear:both;'>
          <h1 style='color:#fff;margin-top:25%;'> No podcasts found! </h1>
        </div>
      </div>  

      <div class='footer' style='clear:both;background-color:rgba(0, 0, 0, 0.5);height:150px;'>
        <div class="col-xs-12 text-center">
          <ul style="line-height: 50px;list-style:none;color:#fff;margin-top:20px;">
            <li>
              <small>© 2019 <a href="http://jpaulet.com/" target="_blank" style="color:#fff;">JP.Aulet</a>. All Rights Reserved.</small>
            </li>
          </ul>
          <ul style='list-style: none;color:#fff;margin:10px auto;text-align: center;line-height:15px;'>
            <li class='col-xs-2 col-xs-offset-3'>
              <a href="https://twitter.com/jp_aulet" target="_blank" style="font-size:12px;color:#fff;text-decoration: none;">
                <img src='https://www.iconsdb.com/icons/preview/white/twitter-xxl.png' style='height:15px;width:15px;'> @jpaulet
              </a>
            </li>
            <li class='col-xs-2'>
              <a href="https://github.com/jpaulet" target="_blank" style="font-size:12px;color:#fff;text-decoration: none;">
                <img src='https://www.iconsdb.com/icons/preview/white/github-11-xxl.png' style='height:15px;width:15px;'> jpaulet
              </a>
            </li>
            <li class='col-xs-3'>
              <a href="http://buymeacoff.ee/mpSEk0R" style="font-size:12px;color:#fff;text-decoration: none;" target="_blank">
                <img src="https://www.roastme.xyz/img/buymecoffee-logo.png" alt="Buy me a coffee" style="margin-top:-8px;"> Buy me a Coffee
              </a>
            </li>
          </ul>        
        </div>
      </div>    
    </div>
  </section>
</template>

<script>
import Podcast from "~/components/Podcast.vue";

export default {
  components: {
    Podcast
  },
  data() {
    return {
      podcasts: null,
      search: '',
      tags: null,
      selectedTags: [],
      showTags: false,
      showPromote:false
    };
  },
  methods: {
    getPodcasts() {
      this.podcasts = require("../data/podcasts.json");
      this.podcasts = this.shuffle(this.podcasts);
    },
    cleanSearch: function(ev){
      this.search = '';
    },
    selectTag: function(event){
      var idx = this.selectedTags.indexOf(event);
      if (idx >= 0) {
        this.selectedTags.splice(idx, 1);
      } else {
        this.selectedTags.push(event);
      }
    },
    shuffle: function(array) {
      var currentIndex = array.length, temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      return array;
    }
  },
  created() {
    this.getPodcasts();
  },
  computed: {
    filteredItems() {
      return this.podcasts.filter(podcast => {        
         return ((podcast.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1) || 
         (podcast.description.toLowerCase().indexOf(this.search.toLowerCase()) > -1)) &&
         (this.selectedTags.length == 0 || podcast.category.trim().toLowerCase().split(',').some(v => { return this.selectedTags.indexOf(v) >= 0; }) )
      });
      //(podcast.category.split(',').some(v => { return this.selectedTags.indexOf(v) >= 0; }) )
    },
    filterTags() {
      let tags = this.podcasts.map(podcast => {
        return podcast.category.trim().toLowerCase().split(',');
      });
      tags = [].concat(...tags);
      tags = tags.sort();
      return tags.filter((v, i, a) => v !== '' && a.indexOf(v) === i);
    }
  }
};
</script>
