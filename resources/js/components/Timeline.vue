<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Timeline</div>
                    <div class="card-body">
                        <post-form></post-form>
                        <hr>
                        <post v-for="post in posts" :key="post.id" :post="post"></post>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Post from './Post'
    import PostForm from './PostForm'
    import bus from '../bus'

    export default {
        data () {
            return {
                posts: []
            } 
        },

        components: {
            Post,
            PostForm
        },

        methods: {
            addPost (post) {
                this.posts.unshift(post)
            }
        },

        mounted() {
            bus.$on('post-added', this.addPost)
            axios.get('/posts').then((response) => {
                this.posts = response.data
            })
        }
    }
</script>
