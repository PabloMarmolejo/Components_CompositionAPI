<script setup>
import { ref } from "vue";

import BlogPost from "./components/BlogPost.vue";

const posts = ref([
    { id: 1, title: "Post 01", body: "Descrión del post 01" },
    { id: 2, title: "Post 02", body: "Descrión del post 02" },
    { id: 3, title: "Post 03" },
]);
</script>

<template>
    <div class="container">
        <h1>Blog</h1>
        <BlogPost
            v-for="post in posts"
            :key="post.title"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            class="mb-2"
        />
    </div>
</template>
