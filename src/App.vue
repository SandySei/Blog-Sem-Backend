<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "Postar aqui não é legal",
        },
        {
          title: "Meu segundo post",
          datetime: Date.now(),
          content: "Postar aqui não é legal",
        },
      ],
      formData: {
        title: "",
        content: "",
      },
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      // se search estiver vazia, retorne a lista completa de posts
      if (!this.search) return this.posts;

      //se tiver qualquer coisa em search, faz o filtro
      const listaFiltrada = [];

      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFiltrada.push(post);
        }
      }
      return listaFiltrada;
    },
  },
  methods: {
    handleClick(event) {
      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {
        title: "",
        content: "",
      };
    },
    handleImputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <input v-model="search" placeholder="Procure pelo título do post..." />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form>
    <input v-model="formData.title" placeholder="Título" />
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      id=""
      cols="30"
      rows="10"
    >
    </textarea>

    <button class="glow-on-hover" type="button" @click="handleClick">
      Salvar
    </button>
  </form>

  <RouterView />
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

form > * {
  margin: 1rem;
}
</style>
