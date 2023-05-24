<script>
import "@/assets/base.css";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "\ud83d\udcc6 18/5/2023 \ud83d\udd52 10:30:17",
          content: "Conteúdo magnifico",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatePost, id) {
      this.posts[id] = updatePost;
    },
    removePost(id) {
      const minhaNovaLista = [];

      for (const index in this.posts) {
        if (index == id) {
          continue;
        }
        const post = this.posts[index];
        minhaNovaLista.push(post);
      }
      this.posts = minhaNovaLista;
    },
  },
};
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/create">Novo Post</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="removePost"
    />
  </main>
</template>

<style scoped>
main {
  padding-top: 70px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
