<script>
import axios from 'axios';
import { store } from '../store.js';

export default {
    name: 'SinglePost',
    data() {
        return {
            store,
            post: null
        };
    },
    methods: {
        getPostDetails() {
            axios.get(`${this.store.apiBaseUrl}/api/posts/${this.$route.params.slug}`)
            .then((response) => {

                if(response.data.success) {
                    this.post = response.data.post;
                } else {
                    this.$router.push({name: 'not-found'});
                }
            });
        }
    },
    mounted() {
        this.getPostDetails();
    }
}
</script>

<template>
    <div class="container">
        <div v-if="post">
            <h1>{{ post.title }}</h1>

            <div v-if="post.cover_image">
                <img :src="`${this.store.apiBaseUrl}/storage/${post.cover_image}`" :alt="post.title">
            </div>

            <p v-if="post.content">
                {{ post.content }}
            </p>
        </div>
    </div>
</template>
