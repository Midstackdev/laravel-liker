<template>
	<div>
		<div class="media">
		  <img :src="post.user.avatar" class="mr-3" :alt="post.user.mame">
		  <div class="media-body">
		    <strong>{{ post.user.name }}</strong>
		   <p> {{ post.body }}</p>
		  </div>
		</div>
	</div>
</template>

<script>
	
	export default {
		props: ['post']
	}
</script>

<style scoped>
	.media {
		position: relative;
		margin: 0;
		padding: 10px;
	}
</style>