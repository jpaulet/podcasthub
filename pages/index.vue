<template>
  <section class="container">
    <div style='height:100%;width:100%;overflow: hidden;'>
      <div class='row headerBanner'>  
        <h1 class="title col-xs-12 col-sm-7">
          podcastStash 
          <fa icon='microphone-alt' />
        </h1>

        <div class='hidden-xs col-sm-5' style='padding:30px 10px;text-align: right;'>
          <a href='https://jpaulet.typeform.com/to/TJOlbG' target='_blank' class='bmc-button' style='font-size:13px;text-decoration: none;margin-right:8px !important;vertical-align:top;'>Add Podcast</a>

          <style>
            .bmc-button img{
              width: 27px !important;
              margin-bottom: 1px !important;
              box-shadow: none !important;
              border: none !important;
              vertical-align: middle !important;
            }
            .bmc-button{
              vertical-align: top;
              line-height: 36px !important;
              height:37px !important;
              text-decoration: none !important;
              display:inline-flex !important;
              color:#000000 !important;
              background-color:#ffffffb5 !important;
              border-radius: 6px !important;
              border: 1px solid transparent !important;
              padding: 0px 9px !important;
              font-size: 17px !important;
              letter-spacing:-0.08px !important;
              box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;
              -webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;
              margin: 5px auto !important;
              font-family:'Lato', sans-serif !important;
              -webkit-box-sizing: border-box !important;
              box-sizing: border-box !important;
              -o-transition: 0.3s all linear !important;
              -webkit-transition: 0.3s all linear !important;
              -moz-transition: 0.3s all linear !important;
              -ms-transition: 0.3s all linear !important;
              transition: 0.3s all linear !important;
            }
            .bmc-button:hover, .bmc-button:active, .bmc-button:focus {
              -webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;
              text-decoration: none !important;
              box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;
              opacity: 0.85 !important;
              color:#000000 !important;
            }
          </style>
          <link href="https://fonts.googleapis.com/css?family=Lato&subset=latin,latin-ext" rel="stylesheet">
          <a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/mpSEk0R">
            <img src="https://www.buymeacoffee.com/assets/img/BMC-btn-logo.svg" alt="Support My Work">
            <span style="margin-left:5px">Support My Work</span>
          </a>
        </div>
        

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

        <div class='textWrapper col-xs-12' style='margin-top:25px;margin-bottom:20px;'> 
          <span style='text-decoration: underline;'>Hand-picked</span> list with <span style='font-size:16px;background-color: rgba(255, 255, 255, 0.19);border-radius:6px;padding:3px 6px;'>+{{ podcasts.length }}</span> awesome podcasts for makers, designers, programmers & more! <fa icon='microphone-alt' />
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

<style>
html{
  min-width:362px;
}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #0e2439 !important;
  margin:0px;
}

.headerBanner{
  background-color:rgba(0, 0, 0, 0.5);
  padding:0px 20px;
  height:100px;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 600;
  font-size: 30px;
  letter-spacing: 1px;
  margin-bottom: 10px;
  text-align:left;
  padding:30px 15px;
  color:rgb(156, 179, 201);
  margin-top:2px;
  margin-bottom:0px;
}

.searchInput{
  border-radius:6px;
  border:1px solid #ccc;
  padding:6px 8px;
  box-shadow:none;
  opacity:0.75;
}

.searchInput:focus{
  opacity:1;
  box-shadow: 0 0 5px rgba(81, 203, 238, 1);
}

.filterList{
  margin:20px auto;
  height:30px;
  clear:both;
}

.searchIcon{
  font-size:11px;
  color:rgb(156, 179, 201);
  margin-left:-24px;
  z-index:9999;
  cursor:pointer;
}

.filterTagButton{
  float:left;
  background-color: #c2c8cd; 
  border:0px;
  border-radius:8px;
  padding:7px 10px;
  color:#555;
}

.btn{
  background-color: #c2c8cd; 
  border:0px;
  border-radius:8px;
  padding:7px 10px;
  color:#0e2439;
  margin-top:8px;
  cursor:pointer;
  margin-right:8px;
}

.filterTags{
  float:left;
  width:100%;
  padding:20px 10px;
  clear:both;
}

.tagCheckbox{
  outline:0px;
}

.tagCheckbox .btn{
  display:inline-block;
  font-size:11px;
  color:#eee;
  margin: 3px 5px;
  padding: 3px 6px;
  border-radius: 4px;
  background-color: #ffffff3d;
  cursor:pointer;
}

.tagCheckbox .active{
  background-color: #000;
  box-shadow: 0 0 5px rgba(81, 203, 238, 1);
}

.tagCheckbox label{
  padding:4px;
  margin:-4px;
  cursor:pointer;
}

.tagCheckbox .btn input{
  display:none;
}

.closeButton{
  border-radius:18px;
  border:0px;
  height:20px;
  width:20px;
  line-height:12px;
  font-size:12px;
  float:right;
  cursor:pointer;
}

.expandInfo{
  color:#fff;
  font-size:13px;
  float:left;
  margin-left:55px;
  margin-top:5px;
  height:;
}

.textWrapper{
  color:#fff;
  font-weight: 600;
  margin-top:5px;
}
</style>
