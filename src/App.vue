<script setup>
import { ref } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";

const posts = ref([]);
const postXpage = 10
const inicio = ref(0)
const fin = ref(postXpage)

const favorito = ref()

const cambiarFavorito = (title) => {
  favorito.value = title
}

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}

const Previus = () => {
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => posts.value = data);
</script>

<template>
  <div class="container">
    <h1>Blog</h1>
    <h2>Posts Favoritos {{ favorito }}</h2>

    <button @click="next">Siguiente</button>
    <button @click="Previus">Atrás</button>

    <PaginatePost class="mb-2" />

    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.title" :title="post.title" :id="post.id"
      :body="post.body" class="mb-2" @cambiarFavorito="cambiarFavorito" />
  </div>
</template>
