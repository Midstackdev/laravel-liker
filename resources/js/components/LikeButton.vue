<template>
	<div class="like">
		<button class="btn btn-success btn-sm like__button">Like</button>
	</div>
</template>

<script>
	
	export default {

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