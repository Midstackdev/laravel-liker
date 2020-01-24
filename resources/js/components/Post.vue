<template>
	<div>
		<div class="media">
		<like-button v-if="post.likedByCurrentUser === false && post.canBeLikedByCurrentUser === true" :post="post"></like-button>
		  <img :src="post.user.avatar" class="mr-3" :alt="post.user.mame">
		  <div class="media-body">
		    <strong>{{ post.user.name }}</strong>
		   <p> {{ post.body }}</p>
		   <span> {{ post.likeCount }} {{ pluralize('like', post.likeCount) }}</span>
		  </div>
		</div>
	</div>
</template>

<script>
	import LikeButton from './LikeButton'

	export default {
		props: ['post'],

		components: {
			LikeButton
		}
	}
</script>

<style scoped>
	.media {
		position: relative;
		margin: 0;
		padding: 10px;
	}

	.media:hover .like {
		display: block;
	}
</style>