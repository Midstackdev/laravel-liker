<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Timeline</div>

                    <div class="card-body">
                        <post v-for="post in posts" :key="post.id" :post="post"></post>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Post from './Post'

    export default {
        data () {
            return {
                posts: []
            } 
        },

        components: {
            Post
        },

        mounted() {
            axios.get('/posts').then((response) => {
                this.posts = response.data
            })
        }
    }
</script>
