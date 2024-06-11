<script>
import axios from 'axios';

export default {
    name: 'SinglePost',
    data() {
        return {
            post: null
        };
    },
    methods: {
        getPostDetails() {
            axios.get(`http://127.0.0.1:8000/api/posts/${this.$route.params.slug}`)
            .then((response) => {
                this.post = response.data.post;
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
                <img :src="`http://127.0.0.1:8000/storage/${post.cover_image}`" :alt="post.title">
            </div>

            <p v-if="post.content">
                {{ post.content }}
            </p>
        </div>
    </div>
</template>
