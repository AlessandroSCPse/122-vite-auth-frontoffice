<script>
export default {
    name: 'SinglePost',
    props: {
        postDetails: Object
    }
}
</script>

<template>
    <div class="col">
        <div class="card my-3">
            <!-- <img src="..." class="card-img-top" alt="..."> -->
            <div class="card-body">
                <h5 class="card-title">{{ postDetails.title }}</h5>
                <div v-if="postDetails.category">
                    <strong>Categoria</strong>: {{ postDetails.category.name }}
                </div>

                <div v-if="postDetails.tags.length > 0">
                    <strong>Tags</strong>: <span v-for="tag in postDetails.tags">{{ tag.name }} &nbsp;</span>
                </div>
                <p v-if="postDetails.content" class="card-text">{{ postDetails.content }}</p>
                 <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
            </div>
        </div>
    </div>
</template>
