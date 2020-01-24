<template>
	<div>
		<form @submit.prevent="post">
			<div class="mb-3">
			  <!-- <label for="validationTextarea">Textarea</label> -->
			  <textarea class="form-control" cols="30" rows="3" placeholder="Write someting likeable" v-model="body"></textarea>
			  <!-- <div class="invalid-feedback">
			    Please enter a message in the textarea.
			  </div> -->
			</div>
			<button class="btn btn-primary" type="submit">Post it!</button>
		</form>
	</div>
</template>

<script>
	import bus from '../bus'

	export default {
		data () {
			return {
				body: ''
			}
		},
		methods: {
			post () {
				axios.post('/posts', {
					body: this.body
				}).then((response) => {
					bus.$emit('post-added', response.data)
					this.body = ''
				})
			}
		}
	}
</script>