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
            currentPage: 1,
            prevPageUrl: null,
            nextPageUrl: null,
            posts: []
        };
    },
    methods: {
        getPosts(pageNumber) {
            axios.get('http://127.0.0.1:8000/api/posts', {
                params: {
                    page: pageNumber
                }
            })
            .then((response) => {
                this.posts = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.prevPageUrl = response.data.results.prev_page_url;
                this.nextPageUrl = response.data.results.next_page_url;
            });
        }
    },
    mounted() {
        this.getPosts(this.currentPage);
    }
}
</script>

<template>
    <div class="container">
        <h1>Tutti i post</h1>
        {{ currentPage }}
        <div class="row row-cols-3">
            <SinglePost v-for="post in posts" :postDetails="post" :key="post.id"></SinglePost>
        </div>

        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li v-if="prevPageUrl" class="page-item">
                    <a class="page-link" @click="getPosts(currentPage - 1)">Previous</a>
                </li>
                <li v-if="nextPageUrl" class="page-item">
                    <a class="page-link" @click="getPosts(currentPage + 1)">Next</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style scoped lang="scss">
</style>
