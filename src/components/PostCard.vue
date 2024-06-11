<script>
export default {
    name: 'PostCard',
    props: {
        postDetails: Object
    },
    methods: {
        truncateText(text) {
            // Se il testo è più lungo di 100 caratteri
            // lo taglio a 100 caratteri e aggiungo ...
            // altrimenti il testo non lo tocco
            if(text.length > 100) {
                return text.substr(0, 99) + '...';
            }

            return text;
        }
    }
}
</script>

<template>
    <div class="card my-3">
        <div class="card-body">
            <h5 class="card-title">{{ postDetails.title }}</h5>
            <div v-if="postDetails.category">
                <strong>Categoria</strong>: {{ postDetails.category.name }}
            </div>

            <div v-if="postDetails.tags.length > 0">
                <strong>Tags</strong>: <span v-for="tag in postDetails.tags">{{ tag.name }} &nbsp;</span>
            </div>
            <p v-if="postDetails.content" class="card-text">{{ truncateText(postDetails.content) }}</p>
            <router-link :to="{ name: 'single-post', params: {slug: postDetails.slug } }" class="btn btn-primary">Read more</router-link>
        </div>
    </div>
</template>
