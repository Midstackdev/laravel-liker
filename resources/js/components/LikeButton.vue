<template>
	<div class="like">
		<button type="button" class="btn btn-success btn-sm like__button" @click.prevent="like">Like</button>
	</div>
</template>

<script>
	import bus from '../bus'

	export default {
		props: ['post'],
		methods: {
			like () {
				axios.post(`/posts/${this.post.id}/likes`).then((response) => {
					bus.$emit('post-liked', this.post.id, true)
				})
			}
		}
	}
</script>

<style scope>
	.like {
		display: none;
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0; left: 0;
		background: rgba(0, 0, 0, .05);
		border-radius: 3px;
		box-sizing: border-box;
	}

	.like__button {
		position: absolute;
		top: 50%;
		right: 20px;
		transform: translate(0, -50%);		
	}
</style>