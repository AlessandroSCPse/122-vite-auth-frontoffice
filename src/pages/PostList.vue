<script>
import axios from 'axios';
import { store } from '../store.js';
import PostCard from '../components/PostCard.vue';
import Loader from '../components/Loader.vue';

export default {
    name: 'PostList',
    components: {
        PostCard,
        Loader
    },
    data() {
        return {
            store,
            currentPage: 1,
            prevPageUrl: null,
            nextPageUrl: null,
            posts: [],
            loading: false
        };
    },
    methods: {
        getPosts(pageNumber) {
            this.loading = true;

            axios.get(`${this.store.apiBaseUrl}/api/posts`, {
                params: {
                    page: pageNumber
                }
            })
            .then((response) => {
                this.posts = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.prevPageUrl = response.data.results.prev_page_url;
                this.nextPageUrl = response.data.results.next_page_url;
                this.loading = false;
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

        <div v-if="!loading" class="row row-cols-3">
            <div class="col" v-for="post in posts" :key="post.id">
                <PostCard :postDetails="post"></PostCard>
            </div>
        </div>
        <div v-else>
            <Loader></Loader>
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
