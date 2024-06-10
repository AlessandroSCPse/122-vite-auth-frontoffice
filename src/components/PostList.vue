<script>
import axios from 'axios';
import SinglePost from './SinglePost.vue';

export default {
    name: 'PostList',
    components: {
        SinglePost
    },
    data() {
        return {
            posts: []
        };
    },
    methods: {
        getPosts() {
            axios.get('http://127.0.0.1:8000/api/posts')
            .then((response) => {
                this.posts = response.data.results;
            });
        }
    },
    mounted() {
        this.getPosts();
    }
}
</script>

<template>
    <div class="container">
        <h1>Tutti i post</h1>

        <div class="row row-cols-3">
            <SinglePost v-for="post in posts" :postDetails="post" :key="post.id"></SinglePost>
        </div>
    </div>
</template>

<style scoped lang="scss">
</style>
