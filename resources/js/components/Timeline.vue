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
            },

            likePost (postId, likedByCurrentUser) {
                let i

                for (i = 0; i <= this.posts.length; i++) {
                    if (this.posts[i].id === postId) {
                        this.posts[i].likeCount++

                        if (likedByCurrentUser) {
                            this.posts[i].likedByCurrentUser = true
                        }

                        break;
                    }
                }
            }
        },

        mounted() {
            bus.$on('post-added', this.addPost)
            bus.$on('post-liked', this.likePost)

            axios.get('/posts').then((response) => {

                Echo.private('posts').listen('PostWasCreated', (e) => {
                    // console.log(e.post)
                    bus.$emit('post-added', e.post)
                })

                Echo.private('likes').listen('PostWasLiked', (e) => {
                    // console.log(e.post)
                    bus.$emit('post-liked', e.post.id, false)
                })

                if (window.Notification && Notification.permission !== 'denied') {
                    Notification.requestPermission((status) => {

                        Echo.private(`App.User.${user.id}`).listen('PostWasLiked', (e) => {
                            // console.log(e)
                            new Notification('Post liked', {
                                body: `${e.user.name} liked your post ${e.post.body}`
                            })
                        })
                    })
                }


                this.posts = response.data
            })
        }
    }
</script>
