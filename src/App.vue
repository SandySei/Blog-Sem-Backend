<script>
import "@/assets/base.css";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "T-Rex Running",
          datetime: "\ud83d\udcc6 18/5/2023 \ud83d\udd52 10:30:17",
          content:
            "Jogo do dinossauro do Chrome, pode ser um ótimo passatempo quando não se tem nada para fazer. Ele pode ser acessado tanto quando está offline, como ficou mais conhecido, quanto com internet. Basta digitar “chrome://dino” no navegador do seu computador ou celular.",
        },
        {
          title: "Google finalmente explica origens do jogo do dinossauro no Chrome",
          datetime: "\ud83d\udcc6 20/5/2023 \ud83d\udd52 22:10:18",
          content:
          "Depois de quatro anos de presença no navegador, o Google publicou uma entrevista com os desenvolvedores que criaram este pedaço de procrastinação garantida. Segundo Sebastien Gabriel, um dos responsáveis pela programação do pequeno game, ele “é uma brincadeira focada em voltar à era pré-histórica, quando você não tinha Wi-Fi. Os cenários de cactos e do deserto fizeram parte da primeira iteração da página “você está off-line”, enquanto o estilo visual é um aceno à nossa tradição de pixel-art nas ilustrações de erro do Google Chrome.”"
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
