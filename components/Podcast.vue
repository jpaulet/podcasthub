<template>
	<div class='podcast-box'>
	  <b-card 
	  	:title="podcast.name"
	    :img-src="logo"
	    img-alt="Image"
	    img-top
	    tag="article"
	    style="max-width: 12rem;width:100%;min-width:200px;min-height:122px;overflow:hidden;"
	    class="mb-2"
	    :class="(podcast.logo ? '' : 'shadow')">

	    <b-badge class='podcast-lang'> {{podcast.languages | twoLetter }} </b-badge>

	    <p v-if='podcast.host' class='podcast-host'>by {{podcast.host}}</p> 
	    <p class="card-text">
	      {{podcast.description}}		  
	    </p>
	    <div class='div-tags'>
	      	<tags 
	      		v-for="(tag,index) in podcast.category.split(',')" 
	      		:tag="tag" 
	      		:key="`${podcast.name}-tag-${index}`" />
	    </div>
	    <div class='podcast-url' style='width:95%;overflow:hidden;'>
	    	<b-button :href="podcast.url" variant="primary" target='_blank'>{{podcast.url}}</b-button>
	    	<fa icon="external-link-alt" class='external-link' />
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
  		let rand = Math.floor(Math.random() * (4 - 1 + 1)) + 1;
  		return ( this.podcast.logo ? this.podcast.logo : '/podcast'+rand+'.jpg')
  	}
  },
  filters: {
	twoLetter: function (value) {
		if( value === 'English'){ return 'EN' }
		else if( value === 'Spanish'){ return  'ES' }
		else if( value === 'Portuguese'){ return  'PT' }
		else if( value === 'French'){ return  'FR' }
		else if( value === 'Chinese'){ return  'CH' }
		else { return ''; }
	}
  }
}
</script>

<style scoped>
	.podcast-box{
		display:inline-flex;
		margin:10px 15px;
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
		margin-top:12px;
		text-align:left;
	}
	.podcast-host{
		font-size:11px;
		color:#999;
		text-align:left;
		padding:0px 20px;
	}
	.podcast-lang{
		float:right;
		font-size:9px;
		position:relative;
		top:-16px;
		right:6px;
		cursor:pointer;
	}
	.card-title{
		text-align: left;
		font-size:14px;
		padding:10px 20px 0px;
		width:94%;
	}
	.card-img-top {
	    width: 100%;
	    height: 12vw;
	    max-height:250px;
	    object-fit: cover;
	    border-top-right-radius: 6px;
	    border-top-left-radius: 6px;
	    min-height:120px;
	}
	.card-text{
		padding:10px 20px 15px;
		text-align: justify;
		font-size:12px;
	}
	.shadow > .card-img-top{
		opacity:0.6;
	}
	.external-link{
		display:inline;
		font-size:8px;
		color:#555;
		margin-left:2px;
	}
	.div-tags{
		text-align:left;
		padding:0px 20px;
	}
</style>