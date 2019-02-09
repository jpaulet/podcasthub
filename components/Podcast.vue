<template>
	<div class='podcast-box'>
	  <b-card 
	  	:title="podcast.name"
	    :img-src="logo"
	    img-alt="Image"
	    img-top
	    tag="article"
	    style="max-width: 20rem;width:100%;min-width:200px;min-height:122px;"
	    class="mb-2"
	    :class="(podcast.logo ? '' : 'shadow')">
	    <p class="card-text">
	      {{podcast.description}}		  
	    </p>
	    <div class='div-tags' style='text-align:left;padding:0px 20px;'>
	      	<tags 
	      		v-for="(tag,index) in podcast.category.split(',')" 
	      		:tag="tag" 
	      		:key="`${podcast.name}-tag-${index}`" />
	    </div>
	    <div class='podcast-url'>
	    	<span style='font-size:9px;'>Site:</span> 
	    	<b-button :href="podcast.url" variant="primary" target='_blank'>{{podcast.url}}</b-button>
	    </div>
	  </b-card>
	</div>
</template>

<script>	
import Tags from '~/components/Tags.vue'

export default {
  components: {
    Tags
  },
  props: [ 'podcast' ],	  
  computed: {
  	logo: function(){
  		let rand = Math.floor(Math.random() * (3 - 1 + 1)) + 1;
  		return ( this.podcast.logo ? this.podcast.logo : '/podcast'+rand+'.jpg')
  	}
  }
}
</script>

<style scoped>
	.podcast-box{
		display:inline-flex;
		margin:10px;
		border-radius:6px;
		box-shadow: 0 0.5px 0 0 #ffffff inset, 0 1px 2px 0 #B3B3B3;
	}
	.podcast-box:hover{
		-webkit-box-shadow: 0 3px 2px #777;
		-moz-box-shadow: 0 3px 2px #777;
		box-shadow: 0 3px 2px #777;
	}
	.podcast-url{
		float:left;
		padding-left:22px;
		margin-bottom:10px;
		font-size:12px;
		margin-top:8px;
	}
	.card-title{
		text-align: left;
		font-size:13px;
		padding:10px 20px 0px;
	}
	.card-img-top {
	    width: 100%;
	    height: 30vw;
	    max-height:250px;
	    object-fit: cover;
	    border-top-right-radius: 6px;
	    border-top-left-radius: 6px;
	}
	.card-text{
		padding:20px;
		text-align: justify;
		font-size:12px;
	}
	.shadow.card-img-top{
		background-color: #ffffff70;
	}
</style>