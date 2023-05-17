<script>
import "@/assets/base.css";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost)
    },
  },
};
</script>

<template>
  <RouterLink to="/">Home</RouterLink>
  <RouterLink to="/create">Novo Post</RouterLink>

  <RouterView :posts="posts" @create-post="addPost" />
</template>

<style scoped></style>
