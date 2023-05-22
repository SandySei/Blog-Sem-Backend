<script>
import "@/assets/base.css";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "18/5/2023",
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
header {
  background: linear-gradient(
    360deg,
    rgba(255, 255, 255, 1) 0%,
    rgba(0, 0, 0, 0.7) 100%
  );

  position: absolute;
  width: 100vw;

  top: 0;
  left: 0;
}
a {
  color: #000000;
  text-decoration: none;
  font-weight: bolder;
  letter-spacing: 0.5px;

  width: 50%;
  height: 40px;
  border: none;
  outline: none;
  cursor: pointer;
  position: relative;
  z-index: 0;

  display: flex;
  justify-content: center;
  align-items: center;

  -webkit-transition: all 0.5s ease;
  transition: all 0.5s ease;
}

a:hover {
  color: #0018b3;
  -webkit-transform: scale(1.2);
  transform: scale(1.2);
  letter-spacing: 1px;
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
}

main {
  padding-top: 90px;
}
</style>
