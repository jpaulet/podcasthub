<template>
	<b-badge @click='filterTags(tag)' variant="secondary">{{tag}}</b-badge>
</template>

<script>
	export default{
		props: [ 'tag' ]
	}
</script>

<style>
	.badge{
		font-size:11px;
		margin-right:6px;
		border:1px solid #ccc;
		padding:1px 3px;
		background-color: #eee;
		border-radius:6px;
		color:#333;
		text-decoration: none;
		display:inline-block;
	}
</style>